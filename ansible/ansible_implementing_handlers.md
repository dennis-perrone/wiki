# Implementing Handlers within Ansible

## Notes

- Handlers are triggered as part of a task and run after the play finishes.
- You can specify a `force_handlers: true` option in the header to require the handlers to execute.
  - This is valid both at a **play** and at a **task** level.
  - This will force the handlers to run if the play previously failed but triggering changes were made prior to failure.
- They are referred to by their name.
- They exist within a *per-play* namespace.
- You can trigger handlers to run before the end of the play by using the `ansible.builtin.meta flush_hanlders` module.
