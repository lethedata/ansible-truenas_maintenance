# ansible-truenas_maintenance
Execute TrueNAS tasks via Ansible without additional Galaxy collections by making use of API calls and supported commands.

## Project Focus:
- **Don't use Galaxy collections:** Playbooks should be updateable immediately when something breaks. They shouldn't be left broken until an external project gets updated.
- **Don't perform unsupported commands:** Basically don't do anything that could break TrueNAS such as performing most cli commands or manually manipulating files.
- **Automate Routine Tasks:** Focus is on basic routine maintenance tasks such as system and app updates. All other configurations are done directly through GUI or API calls. Custom playbooks can also be created based on how these playbooks function.

## Implementation Notes:
- API calls are handled by the `ansible.builtin.command` module running `midclt` commands. This let's the remote system "configure itself" which allows better integration with how ansible functions.
- To handle current status of executed jobs, `midclt` calls are put in an `until` loop until the desired state is able to be queried.