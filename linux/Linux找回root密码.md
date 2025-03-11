步骤:
1. 在 linux 登录界面前键盘输入 `E`
2. 在 linux 16 代码后输入 `init=/bin/sh`
3. 键盘输入 `ctrl+X` 进入单用户模式
4. 输入  `mount -o remount, rw /` 
5. 输入 `password`
6. 输入新密码
7. 在光标闪烁位置输入: `touch /. autorelabel`
8. 输入 `exec /sbin/init`