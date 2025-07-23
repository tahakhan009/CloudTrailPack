flowchart TD

subgraph pack[AWS SecLake OCSF to CEF Pack]
    direction LR
    cloudtrail[CloudTrail Logs] --> cloudtrail_filter(["_raw.includes('cloudTrailLogs')"]) --> ocsf_to_cef_cloudtrail
    vpc[VPC Flow Logs] --> vpc_filter(["_raw.includes('vpcFlowLogs')"]) --> ocsf_to_cef_vpc
    route53[Route 53 Logs] --> route53_filter(["_raw.includes('route53')"]) --> ocsf_to_cef_route53
    securityhub[Security Hub Findings] --> securityhub_filter(["_raw.includes('securityHubFindings')"]) --> ocsf_to_cef_securityhub
    pan[Palo Alto Firewall Logs] --> pan_filter(["_raw.includes('panFirewallLogs')"]) --> ocsf_to_cef_pan
end

seclake{{Security Lake Source (OCSF)}} --> main_route[AWS SecLake OCSF Route] --> filter_main;
filter_main(["/cloudTrailLogs|vpcFlowLogs|route53|securityHubFindings|panFirewallLogs/.test(_raw)"]) --> pack;
pack --> output{{CEF Destination (e.g., Sentinel)}}
