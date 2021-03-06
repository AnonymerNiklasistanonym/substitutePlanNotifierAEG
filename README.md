# SubstitutePlanNotifierAEG
With this python script you can detect whether there is a new AEG Böblingen substitute plan public or not.

**Virtual environment:** [How to setup and use `virtualenv` to run this script](VIRTUALENV.md)

**GIT submodule:** [How to update, setup and use the SimplifiedGmailApi submodule](SUBMODULE_INSTRUCTIONS.md)



## Credits and info

This whole project is based on the work of [denniskeller](https://github.com/denniskeller). 
He was the one that helped me create this python script and every now and then still helps me.
Thx :smile: :thumbsup: 

It has it's origins in the [Raspberry Pi 3 tutorial for beginners](https://github.com/AnonymerNiklasistanonym/RaspiForBeginners) repository which I and some others started recently.



## How to host this service yourself

Original this service was developed and run on a Raspberry Pi 3 with Raspbian.

Because the script is very simple you obviously can also use an even less performant computer that runs 24/7 and has Linux.

The script itself is not a loop that waits every 5 minutes, it gets executed - checks plans, sends mails - and quits instantly after that.

### How to add other class plans and recipients?

This is very simple because the data isn't in the script but get's loaded each time from a JSON file.

`data/websites.json`:

```json
[
	{
		"name": "6a",
		"url": "http://www.aeg-boeblingen.de/vertretungsplan/HTML/2_Ver_Kla_AEG_06A.htm",
		"recipients": ["a.cool.email@address.com", "evenmore@cool.com"]
	},
    {
		"name": "11",
		"url": "http://www.aeg-boeblingen.de/vertretungsplan/HTML/2_Ver_Kla_AEG_11.htm",
		"recipients": ["your.email@gnail.com"]
	}
]
```

Simply add another entry or email address and on the next run of the script you are ready to go.

(Obviously the "name" shouldn't be two times the same - if it is you will get errors)

### The change detection

Through the time-based job scheduler `Cron` the hosting is enabled.

Just install the GUI and run it:

```
pi@raspberrypi:~ $ sudo apt-get update && sudo apt-get install gnome-schedule  
pi@raspberrypi:~ $ gnome-schedule 
```

Then copy the script and the folder `data` into your home directory folder under `Documents/SubstitutePlanNotifierAEG`.

Now just create a new `Cron`-job with the command 
`python Documents/SubstitutePlanNotifierAEG/script.py` and say this job should be executed every 5/10/60 minutes.

## The Gmail API extension

If you want to send on every change a email to yourself or others follow this quick tutorial (not really needed but it's quite short and you get it after that better):
https://developers.google.com/gmail/api/quickstart/python

### How to use the SimplifiedGmailApi?

* You can use the `SimplifiedGmailApi` by setting `USE_GMAIL= True` at the start of the main script.
* If you download the repository and the submodule folder is empty enter this:

```
$ git submodule update --init --recursive
```

* Also follow the comments in the script (or even better open the README.md in the submodule folder and follow it) so that you have for your Google account all the files to use the API (`project-name.json`, `client_secret.json`)

After that you get the original API copied and then you can use it.

### How to change the email template?

This is now very simple. Just keep an eye on the comments (don't delete them and if you delete sections you need to set tem somewhere else where it makes sense) and change everything like you want in the `data/email.html` file.

Because if you after this step execute the script `data/html_email_to_html_json.py` the email html file will be perfectly converted to the `html.json` file which you can also edit and the program every run read.



## Questions or Ideas

1. This repository is under the MIT license which means you can copy everything and use it, change it, do whatever you want.
2. But if you have any good ideas you can also contribute to this repository which would be really cool :)
3. If you have any questions or issues send me an email or open an issue.
