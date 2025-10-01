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
    
    for level1, _events in events map {
        if [_events][type] == "accountUpdated" {
            if [_events][id] != "" {
                mutate {
                    replace => {
                        "_idaccountupdated.value" => "%{_events.id} (log #%{level1})"
                    }
                    on_error => "_error.replace._idaccountupdated.value"
                }
                mutate {
                    replace => {
                        "_idaccountupdated.key" => "Account Updated ID (log #%{level1})"
                    }
                    on_error => "_error.replace._idaccountupdated.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_idaccountupdated"
                    }
                }
                mutate {
                    remove_field => ["_idaccountupdated"]
                }
            }
            if [_events][apiKey] == "<API KEY HERE>" {
                mutate {
                    replace => {
                        "event.idm.read_only_udm.metadata.product_deployment_id" => "<API_PRODUCT_NAME_HERE>"
                    }
                }
            } else if [_events][apiKey] == "<API KEY HERE>" {
                mutate {
                    replace => {
                        "event.idm.read_only_udm.metadata.product_deployment_id" => "<API_PRODUCT_NAME_HERE>"
                    }
                }
            } else if [_events][apiKey] =~ "<API KEY HERE>" {
                mutate {
                    replace => {
                        "event.idm.read_only_udm.metadata.product_deployment_id" => "<API_PRODUCT_NAME_HERE>"
                    }
                }
            } else if [_events][apiKey] =~ "<API KEY HERE>" {
                mutate {
                    replace => {
                        "event.idm.read_only_udm.metadata.product_deployment_id" => "<API_PRODUCT_NAME_HERE>"
                    }
                }
            } else if [_events][apiKey] =~ "<API KEY HERE>" {
                mutate {
                    replace => {
                        "event.idm.read_only_udm.metadata.product_deployment_id" => "<API_PRODUCT_NAME_HERE>"
                    }
                }
            } else if [_events][apiKey] =~ "<API KEY HERE>" {
                mutate {
                    replace => {
                        "event.idm.read_only_udm.metadata.product_deployment_id" => "<API_PRODUCT_NAME_HERE>"
                    }
                }
            }
            if [_events][data][uid] != "" {
                mutate {
                    replace => {
                        "_uidaccountupdated.value" => "%{_events.data.uid} (log #%{level1})"
                    }
                    on_error => "_error.replace._uidaccountupdated.value"
                }
                mutate {
                    replace => {
                        "_uidaccountupdated.key" => "Account Updated UID (log #%{level1})"
                    }
                    on_error => "_error.replace._uidaccountupdated.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_uidaccountupdated"
                    }
                }
                mutate {
                    remove_field => ["_uidaccountupdated"]
                }
            }
        }
        if [_events][type] == "accountLoggedIn" {
            if [_events][id] != "" {
                mutate {
                    replace => {
                        "_idaccountloggedin.value" => "%{_events.id} (log #%{level1})"
                    }
                    on_error => "_error.replace._idaccountloggedin.value"
                }
                mutate {
                    replace => {
                        "_idaccountloggedin.key" => "Account Logged In ID (log #%{level1})"
                    }
                    on_error => "_error.replace._idaccountloggedin.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_idaccountloggedin"
                    }
                }
                mutate {
                    remove_field => ["_idaccountloggedin"]
                }
            }
            if [_events][data][uid] != "" {
                mutate {
                    replace => {
                        "_uidaccountloggedin.value" => "%{_events.data.uid} (log #%{level1})"
                    }
                    on_error => "_error.replace._uidaccountloggedin.value"
                }
                mutate {
                    replace => {
                        "_uidaccountloggedin.key" => "Account Logged In ID (log #%{level1})"
                    }
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_uidaccountloggedin"
                    }
                }
                mutate {
                    remove_field => ["_uidaccountloggedin"]
                }
            }
        }
        if [_events][type] == "consentUpdated" {
            if [_events][id] != "" {
                mutate {
                    replace => {
                        "_idconsentupdated.value" => "%{_events.id} (log #%{level1})"
                    }
                    on_error => "_error.replace._idconsentupdated.value"
                }
                mutate {
                    replace => {
                        "_idconsentupdated.key" => "Consent Updated ID(log #%{level1})"
                    }
                    on_error => "_error.replace._idconsentupdated.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_idconsentupdated"
                    }
                }
                mutate {
                    remove_field => ["_idconsentupdated"]
                }
            }
            if [_events][data][uid] != "" {
                mutate {
                    replace => {
                        "_uidconsentupdated.value" => "%{_events.data.uid} (log #%{level1})"
                    }
                    on_error => "_error.replace._uidconsentupdated.value"
                }
                mutate {
                    replace => {
                        "_uidconsentupdated.key" => "Consent Updated UID (log #%{level1})"
                    }
                    on_error => "_error.replace._uidconsentupdated.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_uidconsentupdated"
                    }
                }
                mutate {
                    remove_field => ["_uidconsentupdated"]
                }
            }
            if [_events][data][Action] != "" {
                mutate {
                    replace => {
                        "_actionconsentupdated.value" => "%{_events.data.Action} (log #%{level1})"
                    }
                    on_error => "_error.replace._actionconsentupdated.value"
                }
                mutate {
                    replace => {
                        "_actionconsentupdated.key" => "Consent Updated Action (log #%{level1})"
                    }
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_actionconsentupdated"
                    }
                }
                mutate {
                    remove_field => ["_actionconsentupdated"]
                }
            }
        }
        if [_events][type] == "accountRegistered" {
            if [_events][id] != "" {
                mutate {
                    replace => {
                        "_idaccountregistered.value" => "%{_events.id} (log #%{level1})"
                    }
                    on_error => "_error.replace._idaccountregistered.value"
                }
                mutate {
                    replace => {
                        "_idaccountregistered.key" => "Account Registred ID (log #%{level1})"
                    }
                    on_error => "_error.replace._idaccountregistered.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_idaccountregistered"
                    }
                }
                mutate {
                    remove_field => ["_idaccountregistered"]
                }
            }
            if [_events][data][uid] != "" {
                mutate {
                    replace => {
                        "_uidaccountregistered.value" => "%{_events.data.uid} (log #%{level1})"
                    }
                    on_error => "_error.replace._uidaccountregistred.value"
                }
                mutate {
                    replace => {
                        "_uidaccountregistered.key" => "Account Registered UID (log #%{level1})"
                    }
                    on_error => "_error.replace._uidaccountregistered.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_uidaccountregistered"
                    }
                }
                mutate {
                    remove_field => ["_uidaccountregistered"]
                }
            }
        }
        if [_events][type] == "accountCreated" {
            if [_events][id] != "" {
                mutate  {
                    replace => {
                        "_idaccountcreated.value" => "%{_events.id} (log #%{level1})"
                    }
                    on_error => "_error.replace._idaccountcreated.value"
                }
                mutate {
                    replace => {
                        "_idaccountcreated.key" => "Account Created ID (log #%{level1})"
                    }
                    on_error => "_error.replace._idaccountcreated.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_idaccountcreated"
                    }
                }
                mutate {
                    remove_field => ["_idaccountcreated"]
                }
            }
            if [_events][data][uid] != "" {
                mutate {
                    replace => {
                        "_uidaccountcreated.value" => "%{_events.data.uid} (log #%{level1})"
                    }
                    on_error => "_error.replace._uidaccountcreated.value"
                }
                mutate {
                    replace => {
                        "_uidaccountcreated.key" => "Account Created UID (log #%{level1})"
                    }
                    on_error => "_error.replace._uidaccountcreated.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_uidaccountcreated"
                    }
                }
                mutate {
                    remove_field => ["_uidaccountcreated"]
                }
            }
        }
        if [_events][type] == "accountPasswordChanged" {
            if [_events][id] != "" {
                mutate {
                    replace => {
                        "_idaccountpasswordchanged.value" => "%{_events.id} (log #%{level1})"
                    }
                    on_error => "_error.replace._idaccountpasswordhanged.value"
                }
                mutate {
                    replace => {
                        "_idaccountpasswordchanged.key" => "Account Password Changed (log #%{level1})"
                    }
                    on_error => "_error.replace._idaccountpasswordchanged.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_idaccountpasswordchanged"
                    }
                }
                mutate {
                    remove_field => ["_idaccountpasswordchanged"]
                }
            }
            if [_events][data][uid] != "" {
                mutate {
                    replace => {
                        "_uidaccountpasswordchanged.value" => "%{_events.data.uid} (log #%{level1})"
                    }
                    on_error => "_error.replace._uidaccountpasswordchanged.value"
                }
                mutate {
                    replace => {
                        "_uidaccountpasswordchanged.key" => "Account Password Changed UID (log #%{level1})"
                    }
                    on_error => "_error.replace._uidaccountpasswordchanged.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_uidaccountpasswordchanged"
                    }
                }
                mutate {
                    remove_field => ["_uidaccountpasswordchanged"]
                }
            }
            if [_events][data][newPassword][created] != "" {
                mutate {
                    replace => {
                        "_newpasswordaccountcreated.value" => "%{_events.data.newPassword.created} (log #%{level1})"
                    }
                    on_error => "_error.replace._newpasswordcreated.value"
                }
                mutate {
                    replace => {
                        "_newpasswordaccountcreated.key" => "Account Password Changed New Created Date (log #%{level1})"
                    }
                    on_error => "_error.replace._newpasswordcrated.key"
                }
                mutate {
                    merge => {
                        "event.idm.read_only_udm.principal.resource.attribute.labels" => "_newpasswordaccountcreated"
                    }
                }
                mutate {
                    remove_field => ["_newpasswordaccountcreated"]
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