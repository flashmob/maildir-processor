# MailDir processor for Go-guerrilla MTA.

Maildir is a pupular email storage format.

## About

This package is a _Processor_ for the Go-Guerrilla default `Backend` interface implimentation. Typical use for this
package is if you would like to add the ability to deliver emails to Maildir folders, using the Go-Guerrilla MTA as a package. 

## Usage

Import

 `"github.com/flashmob/maildiranasaurus"` to your Go-guerrilla project. Import `"github.com/flashmob/go-guerrilla/backends"` 
assuming your have done already already.

Somewhere at the top of your code, maybe in your init() function, add

`backends.Svc.AddProcessor("MailDir", maildiranasaurus.MaildirProcessor)`

This will let Go-Guerrilla know about your MailDir processor.

See configuration section for how to configure. Send your configuration to Go-Guerrilla's backends.New() function.


## Configuration

The following values are required in your `backend_config` section

* `maildir_path` - string. maildir_path may contain a [user] placeholder. This will be substituted at run time
eg /home/[user]/Maildir will get substituted to /home/test/Maildir for test@example.com
* `maildir_user_map` - string. This is a string holding user to group/id mappings - in other words, the recipient table
Each record separated by "," where Records have the following format: `<username>=<id>:<group>`<br>
Example: `"test=1002:2003,guerrilla=1001:1001"`

Don't forget to add `MailDir` to the end of your `process_stack` config option
## Example

Take a look at [Maildiranasaurus](https://github.com/flashmob/maildiranasaurus) - an SMTP server that uses Go-Guerrilla as a 
package and adds Maildir processing using this package.


 
