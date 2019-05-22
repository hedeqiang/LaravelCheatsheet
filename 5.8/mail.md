# Mail

---

```php
Mail::send('email.view', $data, function($message){});
Mail::send(array('html.view', 'text.view'), $data, $callback);
Mail::queue('email.view', $data, function($message){});
Mail::queueOn('queue-name', 'email.view', $data, $callback);
Mail::later(5, 'email.view', $data, function($message){});
// 临时将发送邮件请求写入 log，方便测试
Mail::pretend();
```

### 消息

```php
// 这些都能在 $message 实例中使用, 并可传入到 Mail::send() 或 Mail::queue()
$message->from('email@example.com', 'Mr. Example');
$message->sender('email@example.com', 'Mr. Example');
$message->returnPath('email@example.com');
$message->to('email@example.com', 'Mr. Example');
$message->cc('email@example.com', 'Mr. Example');
$message->bcc('email@example.com', 'Mr. Example');
$message->replyTo('email@example.com', 'Mr. Example');
$message->subject('Welcome to the Jungle');
$message->priority(2);
$message->attach('foo\bar.txt', $options);
// 使用内存数据作为附件
$message->attachData('bar', 'Data Name', $options);
// 附带文件，并返回 CID
$message->embed('foo\bar.txt');
$message->embedData('foo', 'Data Name', $options);
// 获取底层的 Swift Message 对象
$message->getSwiftMessage();
              
```