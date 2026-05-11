# Rust Queue - a bounded FIFO message queue as a Linux kernel module
## Spring 2026, Operating Systems - CMSI 3510

<img width="788" height="621" alt="Screenshot 2026-05-08 at 9 45 42 AM" src="https://github.com/user-attachments/assets/4c46bb5a-5a4b-475b-a79e-a7d3bcde8967" />

`rustqueue` is a Linux kernel module that exposes a bounded FIFO message queue at `/dev/rustqueue`, written in safe Rust. It demonstrates how Rust's ownership and locking discipline make a small in-kernel IPC primitive easy to write and structurally free of buffer-handling bugs.

## Future Work

- **Partial reads.** When the user's buffer is smaller than the next message, leave the unread tail in the queue instead of discarding it.
- **Per-process queues.** Use the `open()` handler to give each process its own queue, or each open file descriptor its own session.
- **Configurable capacity.** Expose `MAX_MESSAGES` as a module parameter (`module_param!`) so users can tune it without recompiling.
- **Non-blocking semantics.** Implement `poll()` so user-space `select`/`epoll` can wait for queue activity efficiently.
- **Persistence.** Serialize queue contents to a file on module unload and restore them on load.

## License
*Licensed GPL-2.0 to match the Linux kernel. See `LICENSE`.*
