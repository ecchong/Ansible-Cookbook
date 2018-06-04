### Lowest precedence to hightest
1. Role default variables
2. Inventory variables
3. Inventory group_vars variables:
4. Inventory host_vars variables:
5. group_vars variables defined in group_vars directory
6. host_vars variables defined in host_vars directory
7. Host facts
8. Registered variables
9. Variables defined via set_facts:
10. Variables defined with -a or --args
11. vars_prompt variables
12. Variables included using vars_files
13. role and include variables
14. Block variables
15. Task variables
16. extra variables