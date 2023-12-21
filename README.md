# SOGo-rule-exclusions-plugin
This plugin contains rule exclusions to fix false positives when using SOGo Groupware with the OWASP Core Rule Set.

## Requirements
- CRS Version 4.0 or newer
- ModSecurity compatable Web Application Firewall

## How to install the plugin
1. Copy and paste the files ``sogo-rule-exclusions-before.conf`` and ``sogo-rule-exclusions-config.conf`` into your CRS plugins folder.

2. Create two wildcards includes after ``crs-setup.conf`` but before loading CRS rules. Create the ``*-config.conf`` includes first, followed by the ``*-before.conf`` includes as shown in the code block below (This only needs to be done once, after that any plugins placed within the plugins folder will automatically be activated).

3. Then reload your WAF to apply the new changes (Restart for Nginx ModSec users)

```
Include /path/to/coreruleset/modsecurity.conf
Include /path/to/coreruleset/crs-setup.conf

Include /path/to/coreruleset/plugins/*-config.conf
Include /path/to/coreruleset/plugins/*-before.conf

Include /path/to/coreruleset/rules/*.conf
```

You can also refer to official CRS documentation on how to install a plugin https://coreruleset.org/docs/concepts/plugins/#how-to-install-a-plugin

## Disabling the plugin
The plugin can be disabled by uncommenting rule 9520000 inside ``plugins/sogo-rule-exclusions-config.conf`` or by removing the includes for this plugin.

## Reporting false positives
If you find a false positive that this plugin does not cover then please open a new issue or pull request, if creating an issue then please include the following details:

1. CRS Version
2. ModSecurity/Coraza Version
3. modsec audit logs
4. what caused the false positive
