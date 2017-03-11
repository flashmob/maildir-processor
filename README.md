# Maildir processor for the [Go-guerrilla](https://github.com/flashmob/go-guerrilla) package.

Maildir is a popular email storage format.

## About

This package is a _Processor_ for the Go-Guerrilla default backend implementation. Use for this in your project
if you are using Go-Guerrilla as a package and you would like to add the ability to deliver emails to Maildir folders, using Go-Guerrilla's default backend. 

## Usage

Import `"github.com/flashmob/maildir-processor"` to your Go-guerrilla project.
Assuming you have imported the go-guerrilla package already, and all dependencies.

Then, when [using go-guerrilla as a package](https://github.com/flashmob/go-guerrilla/wiki/Using-as-a-package), do something like this

```go


cfg := &AppConfig{
    LogFile:      "stderr",
    AllowedHosts: []string{"example.com"},
    BackendConfig: backends.BackendConfig{
        "save_process" : "HeadersParser|Debugger|MailDir",
        "validate_process": "MailDir",
        "maildir_user_map" : "test=-1:-1",
        "maildir_path" : "_test/Maildir",
    },
}
d := Daemon{Config: cfg}
d.AddProcessor("FastCGI", fastcgi_processor.Processor)

d.Start()

// .. keep the server busy..

```

Note that here we've added MailDir to the end of the save_process config option, 
then used the d.AddProcessor api call to register it. Then configured other settings.

See the configuration section for how to configure. 


## Configuration

The following values are required in your `backend_config` section of your JSON configuration file

* `maildir_path` - string. maildir_path may contain a `[user]` placeholder. This will be substituted at run time
eg `/home/[user]/Maildir` will get substituted to `/home/test/Maildir` for `test@example.com`
* `maildir_user_map` - string. This is a string holding user to group/id mappings - in other words, the recipient table,
each record separated by "," where records have the following format: `<username>=<id>:<group>`<br>
Example: `"test=1002:2003,guerrilla=1001:1001"` . Use -1 for `<id>` & `<group>` if you want to ignore these, otherwise get these numbers from /etc/passwd
 
Don't forget to add `MailDir` to the end of your `save_process` config option, eg:

`"save_process": "HeadersParser|Debugger|Hasher|Header|MailDir",`

also add `MailDir` to the end of your `validate_process` config option, eg:

`"validate_process": "MailDir",`

## Example

Take a look at [Maildiranasaurus](https://github.com/flashmob/maildiranasaurus) - an SMTP server that uses Go-Guerrilla as a 
package and adds Maildir delivery using this package.

## Credits

This package depends on Simon Lipp's [Go MailDir](https://github.com/sloonz/go-maildir) package.




 
