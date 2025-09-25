# Still testing - currently not passing 100% on the validation but it works everytime in the preview **SHRUGS**

filter {

    json {
        source => "message"
        array_function => "split_columns"
        on_error => "_error.jsonParsingFailed"
    }

    mutate {
        replace => {
            "event.idm.read_only_udm.metadata.event_type" => "GENERIC_EVENT"
        }
    }
    # Handling for the resource > attributes
    for level1, _resourceLogs in resourceLogs map {
        for level2, _attributes in _resourceLogs.resource.attributes map {
            if [_attributes][key] == "com.splunk.sourcetype" {
                mutate {
                    replace => {
                        "_fields.value.string_value" => "%{_attributes.value.stringValue}"
                    }
                    on_error => "_error.replace._fields.string_value"
                }

                mutate {
                    replace => {
                        "_fields.key" => "%{_attributes.key}"
                    }
                    on_error => "_error.replace._fields.key"
                }

                mutate {
                    merge => {
                        "event.idm.read_only_udm.additional.fields" => "_fields"
                    }
                }
            }
            if [_attributes][key] == "host.name" {
                mutate {
                    replace => {
                        "event.idm.read_only_udm.principal.asset.hostname" => "%{_attributes.value.stringValue}"
                    }
                }
            }
            if [_attributes][key] == "os.type" {
                mutate {
                    replace => {
                        "event.idm.read_only_udm.principal.platform" => "LINUX"
                    }
                }
            }
        }
    }
    # Handling scopeLogs > logRecords > body
    # The repeated values that occur we need to remove_field the label during each loop otherwise we overwrite the value for each iteration with the final value
    for l1, _resourceLogs in resourceLogs map {
        for l2, _scopeRecords in _resourceLogs.scopeLogs map {
            for l3, _logRecords in _scopeRecords.logRecords map {
                if [_logRecords][body][stringValue] =~ /INFO/ {
                    drop {
                        tag => "TAG_NO_SECURITY_VALUE"
                    }
                } else if [_logRecords][body][stringValue] =~ /ERROR/ {
                    drop {
                        tag => "TAG_NO_SECURITY_VALUE"
                    }
                } else {
                    mutate {
                        replace => {
                            "_label.value" => "%{_logRecords.body.stringValue}" 
                        }
                    }
                    mutate {
                        merge => {
                            "event.idm.read_only_udm.principal.resource.attribute.labels" => "_label"
                        }
                    }
                    mutate {
                        remove_field => ["_label"]
                    }
                }
            }
        }
    }
    # Handling the log.file.name
    for j1, _resourceLogs in resourceLogs map {
        for j2, _scopeRecords in _resourceLogs.scopeLogs map {
            for j3 _logRecords in _scopeRecords.logRecords map {
                for j4, _attributes in _logRecords.attributes map {
                    if [_attributes][key] == "log.file.name" {
                        mutate {
                            replace => {
                                "event.idm.read_only_udm.metadata.product_log_id" => "%{_attributes.value.stringValue}"
                            }
                        }
                    }
                }
            }
        }
    }

    mutate {
        merge => {
            "@output" => "event"
        }
    }
}
