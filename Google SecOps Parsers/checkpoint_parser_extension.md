filter {
    grok {
      match => {
        "message" => 'TCP packet out of state="%{DATA:out_of_state_reason}"'
      }
      on_error => "no_out_of_state"
    }
  
    # Creating the UDM field structure properly
    if ![no_out_of_state] {
      mutate {
        replace => {
          "additional_field.key" => "StateReason"
          "additional_field.value.string_value" => "%{out_of_state_reason}"
        }
      }
    
      # Merge output in the UDM field
      mutate {
        merge => {
          "event.idm.read_only_udm.additional.fields" => "additional_field"
        }
      }
    }
  
    # Ensure merge happens regardless of success/failure
    mutate {
      merge => {
        "@output" => "event"
      }
      on_error => "_"
    }
  }