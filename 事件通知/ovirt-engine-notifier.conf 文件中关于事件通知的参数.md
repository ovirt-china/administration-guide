# ovirt-engine-notifier.conf 文件中关于事件通知的参数

事件通知器的配置文件是
`/usr/share/ovirt-engine/services/ovirt-engine-notifier/ovirt-engine-notifier.conf`。

|变量名|默认值|备注|
|------|------|----|
|INTERVAL\_IN\_SECONDS|120|向订阅了事件通知的用户发送通知的时间间隔，以秒为单位。|
|MAIL\_SERVER|无|SMTP 邮件服务器地址。必须填写此变量, 事件通知器才能够正常工作。|
|MAIL\_PORT|25|使用不安全连接的 SMTP 服务器的默认端口是 25。使用安全连接（启用了 SSL）的 SMTP 服务器的默认端口是 465。|
|MAIL\_USER|无|如果 SMTP 服务器启用了 SSL 来验证用户，则此变量必须被设置。在 MAIL\_FROM 变量未被设置的情况下，此变量还将会被用以指定发送邮件的用户地址。有些邮件服务器可能不支持此功能。此变量所填的地址必须为 RFC822 格式。|
|MAIL\_PASSWORD|无|此变量在邮件服务器要求用户验证或者启用了 SSL 的情况下必须被设置。|
|MAIL\_ENABLE\_SSL|false|此变量表示与邮件服务器的通信是否使用 SSL。|
|HTML\_MESSAGE\_FORMAT|false|如果此变量被设置为“true”，则邮件服务器将以 HTML 格式发送事件通知信息。|
|MAIL\_FROM|无|如果邮件服务器支持，则此变量将指定符合 RFC822 格式的“from”地址。|
|MAIL\_REPLY\_TO|无|如果邮件服务器支持，则此变量将指定符合 RFC822 格式的“reply-to”地址。|
|DAYS\_TO\_KEEP\_HISTORY|无|此变量将设置发送通知的事件将在历史记录里面保留的天数。如果此变量未被设置，则该事件将在历史记录里永久保存。|

