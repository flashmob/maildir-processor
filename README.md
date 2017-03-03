# Maildir processor for the [Go-guerrilla](https://github.com/flashmob/go-guerrilla) package.

Maildir is a popular email storage format.

## About

This package is a _Processor_ for the Go-Guerrilla default backend implementation. Use for this in your project
if you are using Go-Guerrilla as a package and you would like to add the ability to deliver emails to Maildir folders, using Go-Guerrilla's default backend. 

## Usage

Import `"github.com/flashmob/maildir-processor"` to your Go-guerrilla project. if not already already, import `"github.com/flashmob/go-guerrilla/backends"` - assuming you have imported the go-guerrilla package already.

Somewhere at the top of your code, maybe in your `init()` function, add:

```go
backends.Svc.AddProcessor("MailDir", maildir_processor.Processor)
```

This will let Go-Guerrilla know about your MailDir processor.

See the configuration section for how to configure. Send your configuration to Go-Guerrilla's backends.New() function.


## Configuration

The following values are required in your `backend_config` section of your JSON configuration file

* `maildir_path` - string. maildir_path may contain a `[user]` placeholder. This will be substituted at run time
eg `/home/[user]/Maildir` will get substituted to `/home/test/Maildir` for `test@example.com`
* `maildir_user_map` - string. This is a string holding user to group/id mappings - in other words, the recipient table,
each record separated by "," where records have the following format: `<username>=<id>:<group>`<br>
Example: `"test=1002:2003,guerrilla=1001:1001"` . Use -1 for `<id>` & `<group>` if you want to ignore these, otherwise get these numbers from /etc/passwd
 
Don't forget to add `MailDir` to the end of your `process_stack` config option, eg:

`"process_stack": "HeadersParser|Debugger|Hasher|Header|MailDir",`

## Example

Take a look at [Maildiranasaurus](https://github.com/flashmob/maildiranasaurus) - an SMTP server that uses Go-Guerrilla as a 
package and adds Maildir delivery using this package.

## Credits

This package depends on Simon Lipp's [Go MailDir](https://github.com/sloonz/go-maildir) package.




 
