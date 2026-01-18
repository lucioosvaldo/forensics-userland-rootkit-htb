## Initial Indicators of Compromise

- Inconsistent directory listings between `ls` and `ls -la`
- <img width="911" height="538" alt="image" src="https://github.com/user-attachments/assets/d6d46343-2608-4d65-adbe-effc7af9fc5c" />
- Hidden paths visible only when bypassing environment variables
- Presence of `/etc/ld.so.preload`
<img width="905" height="39" alt="image" src="https://github.com/user-attachments/assets/8411ae02-014d-40d9-9c7b-ec6fd6402c17" />


These behaviors strongly indicate userland manipulation rather than kernel-level compromise.
