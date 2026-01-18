# how-to-tech-info
How to's and misc science and tech links

## Table of Contents

- [Hosting, Tunneling, Email](#hosting-tunneling)
- [Data algorithms](#data-algorithms)
- [Graphics video](#graphics-video)
- [Security privacy](#security-privacy)
- [Databases SQL](#databases-sql)
- [Remove software you don't need](#remove-software-you-don't-need)
- [3D](#3d)
- [Culture](#culture)
- [Coding examples](#coding-examples)
- [Command line and scripting](#command-line-and-scripting)
- [Hardware](#hardware)
- [Content management](#content-management)
- [Physics](#physics)
- [Biology](#biology)
- [Text editors Emacs vi vim Integrated Development Environment IDE](#text-editors-emacs-vi-vim-integrated-development-environment-ide)
- [Cloud Integrated Development Environment IDE](#cloud-integrated-development-environment-ide)
- [SQL PostgreSQL SQLite](#sql-postgresql-sqlite)
- [Clojure](#clojure)
- [Programming languages](#programming-languages)
- [Education Career](#education-career)
- [Operating Systems](#operating-systems)

#### Hosting Tunneling

[How to setup AWS Lightsail server, and build your own website](https://medium.com/@yuhaocooper/how-to-setup-aws-lightsail-server-and-build-your-own-website-e274721ed1bc)

Scroll halfway down to "Escaping CGNAT with Tunnels":
https://blog.rastrian.dev/post/beyond-the-nat-cgnat-bandwidth-and-practical-tunneling

[Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/)

[A Boring Announcement: Free Tunnels for Everyone](https://blog.cloudflare.com/tunnel-for-everyone/)

Forward all email:
https://serverfault.com/questions/328727/forward-incoming-mail-on-linux-server

Probably best to use Postfix as the top answer suggests. Ubuntu has Postfix docs:

https://help.ubuntu.com/community/Postfix

Simplistic overview using sendmail:

- Set up mx records in DNS
- Install sendmail
Set up /etc/mail/virtusertable with the following forwarding line:

`emailaddress@mydomain.com   otheremail@gmail.com`

What you actually need to do using sendmail:

https://serverfault.com/questions/912648/set-up-email-accounts-that-just-auto-forward-to-another-address/914930#914930


#### Data algorithms

https://en.wikipedia.org/wiki/Gerd_Gigerenzer

Heuristics for improved inferences when knowledge is limited. Topics: risk literacy, risk communication,  Daniel Goldstein, recognition heuristic, take-the-best heuristic.

#### Graphics video

Graphscad is a free nodal editor to create customizable 3D objects for 3D printers
https://graphscad.blogspot.com/

CAD software in your browser
https://github.com/itta611/ChokokuCAD/blob/main/README.md


Create flow diagrams aka sequence diagrams aka actors and messages. It sort of looks like what message passing object oriented programming was initially designed to be. 
https://swimlanes.io/

https://www.blackmagicdesign.com/products/davinciresolve/

DaVinci Resolve 16 tools for editing, new cut page, visual effects, motion graphics, color correction, audio post production, single application, seems to have a free version, Mac, Window, Linux. Maybe a replacement for iMovie? 


https://github.com/yuanqing/vdx

An intuitive CLI for processing video, powered by FFmpeg. Crop, trim, resize, reverse, rotate, strip audio, change the speed, change the frame rate, change the volume, convert to a different file format. Run multiple operations on multiple files concurrently.

https://github.com/3b1b/manim

math algorigthm explain video animation code python explainer Manim is an animation engine for explanatory math videos. Used to create precise animations programmatically, as seen in the videos at 3Blue1Brown. There is also a community maintained version at https://github.com/ManimCommunity/manim/. 

#### Security privacy

Checklist of personal security practices. A nice, curated list of things you can do to be more secure online.

https://github.com/Lissy93/personal-security-checklist

Easily (no client, no download) run a headless browser on a remote server:

https://github.com/dosyago/BrowserGap


The Joy of Cryptography is an undergraduate textbook by Mike Rosulek been writing for CS427, his undergraduate course in cryptography.

http://web.engr.oregonstate.edu/~rosulekm/crypto/


MacOS security and privacy guide, setup and initial configuration of Mac 

https://github.com/drduh/macOS-Security-and-Privacy-Guide#spotlight-suggestions


#### Databases SQL

https://animatesql.com/

Animate SQL query operations on a simple two table example database. Maybe kind of fun and educational?

https://github.com/appsmithorg/appsmith

GUI web db app builder sort of for non-devs? From the repo's readme: "Appsmith is a JavaScript-based visual development platform to build and launch internal tools quickly. Drag-and-drop pre-built widgets, and connect them using JavaScript to create interactive pages. Connect UI to your APIs and Databases to build complex workflows in minutes."

PostgREST serves fully RESTful API works with any existing PostgreSQL database. Clever name combines Postgres and REST. API written in Haskell and the WARP http server.

https://github.com/PostgREST/postgrest


Haskell WARP http server

https://hackage.haskell.org/package/warp


Install a pcre perl compatible regular expression (regexp) library for SQLite

https://stackoverflow.com/questions/5071601/how-do-i-use-regex-in-a-sqlite-query


Falcon, free, open source, SQL editor, inline data visualization. Supports: RedShift, MySQL, PostgreSQL, IBM DB2, Impala, MS SQL, Oracle, SQLite and others.

https://github.com/plotly/falcon

#### Remove software you don't need

Uninstall Oracle Java and related Java Applet Plugin. 

https://java.com/en/download/help/mac_uninstall_java.xml

```bash
sudo rm -fr /Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin
sudo rm -fr /Library/PreferencePanes/JavaControlPanel.prefPane
sudo rm -fr ~/Library/Application\ Support/Oracle/Java
```

`ps aux | grep -i java`

/Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Resources/Java Updater.app/Contents/MacOS/Java Updater -bgcheck

Reboot after uninstall, and launchctl will remove non-existing programs. Before uninstalling, you can see com.oracle.java.Java-Updater in the launchctl list.

`launchctl list | grep java`

```
1861    0       com.oracle.java.Java-Updater
-       0       com.apple.java.InstallOnDemand
```


#### 3D 

Stud.io lego studio graphics 3D

https://www.bricklink.com/v3/studio/download.page

Blender 3D

https://www.blender.org/

Using Blender for 3d architecture

http://blender-archi.tuxfamily.org/Blender_for_Architecture

lego brick 3d software builder (not from LEGO corp)

https://www.leocad.org/

#### Culture

"It's Time to Build" failure warnings prepare for the next event including creating systems federal government bailout money to the people and businesses in need

https://a16z.com/2020/04/18/its-time-to-build/

Manuscript, paper, article, doi, full versions, access options. Scientific research should be free for everyone to read. Sci-Hub supports open publication of research, most of which was paid for with our tax dollars. "the first website in the world to provide mass & public access to research papers". Publishers who hide scientific work behind paywalls would seem to favor their own profit over the welfare of the human race.

https://en.wikipedia.org/wiki/Sci-Hub

https://duckduckgo.com/?t=ffab&q=sci-hub&ia=web

Dengue vaccine, CYD-TDV, sold under the brand name Dengvaxia.
https://en.wikipedia.org/wiki/Dengue_vaccine

Antibody-dependent enhancement, seen in Dengue vaccines. You'll need Sci-hub to read the full text. 
https://doi.org/10.1002%2Frmv.2101

Dengue vaccine: WHO position paper – September 2018 (Error: the link on the WHO page goes to an article about leprosy, not dengue.)
https://apps.who.int/iris/handle/10665/274316

drugs use society teens idle hands busy excitement iceland  education

https://www.weforum.org/agenda/2018/10/iceland-knows-how-to-stop-teen-substance-abuse-but-the-rest-of-the-world-isn-t-listening

open source music media player

https://mpv.io/installation/

Bongo usable buffer-oriented media player for Emacs

http://wikemacs.org/index.php/Media_player#Bongo

Vuiet, the music player and explorer for Emacs

https://github.com/mihaiolteanu/vuiet

#### Coding examples

Mito: the fastest way to do Python data analytics, simply by editing a spreadsheet. Edit a spreadsheet, generate Python code

https://www.trymito.io/

https://docs.trymito.io/

Minimal safe Bash script template

https://betterdev.blog/minimal-safe-bash-script-template/

https://gist.github.com/m-radzikowski/53e0b39e9a59a1518990e76c2bff8038

Regular Expressions for Regular Folk regex for beginners example based visual test cases

https://refrf.shreyasminocha.me/

Vanilla example projects in js javascript not vanillajs

https://github.com/bradtraversy/vanillawebprojects

open source javascript music player play lists api examples

https://521dimensions.com/open-source/amplitudejs

#### Command line and scripting


Copy and paste across machines using GitLab Snippets as a storage backend. Sort of replaces and expands pbcopy, pbpaste, xclip (some of which do not work on headless linux servers)

https://github.com/bradwood/glsnip


A flexible command line tool for instantly deploying user interfaces for simple commands and scripts. Create a GUI for cli scripts on the Mac.

https://github.com/Impedimenta/Suitcase

ssh text based social network sharing art music twitter bot html art

https://tilde.town/wiki/faq.html

#### Hardware

uLisp Raspberry coding example I2C Wireless Message Display

http://forum.ulisp.com/t/wireless-message-display/1062

open source time of flight lidar

https://github.com/iliasam/OpenTOFLidar

#### Content management

Replacing my Octopress blog with 200 lines of Babashka

https://blog.michielborkent.nl/migrating-octopress-to-babashka.html

clojure babashka bb scripting content blog manager markdown

https://github.com/maxvoltar/photo-stream

password manager open source stateless multi platform chrome firefox android github

https://lesspass.com/#/


#### Physics


High accuracy ice cores show climate, weather, human activity

https://www.sciencemag.org/news/2018/11/why-536-was-worst-year-be-alive

Methanol fuel beetle robot platium wire muscle nickel-titanium alloy

https://www.sciencenews.org/article/methanol-fuel-beetle-robot


#### Biology

Rt, a key measure of how fast the virus is growing. Effective Reproduction Number. Decisions should be based on the max error bar, not the centroid of the stat.

https://rt.live/

Ageing reversed RNA induced pluripotent stem cells iPS cells

https://www.sciencedaily.com/releases/2020/03/200324090007.htm

human papillomavirus (HPV)  most effective preventive cure eliminated both genders boys girls male female vaccine vaccinated

https://www.sciencedaily.com/releases/2020/03/200312114139.htm

Larry Brilliat warned about pandemic coronavirus covid-19 ted talk epidemiology n95

https://www.wired.com/story/coronavirus-interview-larry-brilliant-smallpox-epidemiologist/

Endocrine system, nighttime light, estrogen receptors

https://www.sciencedaily.com/releases/2016/04/160403152327.htm

Coronavirus Resource Center

Johns Hopkins experts in global public health, infectious disease, and emergency preparedness have been at the forefront of the international response to COVID-19.

https://coronavirus.jhu.edu/

Graphs stats charts coronavirus covid-19

https://www.worldometers.info/coronavirus/

graphs project coronavirus infection rates and deaths advocating rapid response now

https://covidactnow.org/

Coronavirus epidemic calculator interactive

https://gabgoh.github.io/COVID/index.html

#### Text editors Emacs vi vim Integrated Development Environment IDE

Enhanced Emacs experience, especially for beginners. May be easier and/or more sane than default Emacs. Note that you will probably also have a better experience with Emacs if you get a .emacs configuration file from a friend.

https://github.com/bbatsov/prelude

Clojure auto-complete not in a repl, Emacs Clojure[Script] minor mode powered by clj-kondo

https://www.reddit.com/r/Clojure/comments/g4jo95/announcing_the_first_release_of_anakondo_emacs/

Emacs for MacOS (aka OSX, Apple, Mac). If you have a Mac, this is the Emacs you want. 

https://emacsformacosx.com/

#### Cloud Integrated Development Environment IDE

Are You Ready-To-Code?Start Instantly. Anywhere. Gitpod launches ready-to-code dev environments
for your GitHub or GitLab project with a single click.

https://gitpod.io/

See also: Cloud9, AWS LightSail

#### SQL PostgreSQL SQLite

SQLite, shell (bash). Quick, fun intro programming demos, working examples. A short intro to SQL using SQLite. This should work fine for all Mac users since SQLite is pre-installed by Apple. Windows users might have to install SQLite.

https://github.com/twl8n/intro_exercises



#### Clojure

Circular Programming in Clojure. Lambda calculus, interpreters, laziness, monads. Anaylsis of a paper that implements embedded functional languages in Haskell. 
https://cuddly-octo-palm-tree.com/posts/2021-11-21-circular-clojure/

Online Clojure compiler, Online Clojure IDE, and online Clojure REPL. Code Clojure, compile Clojure, run Clojure, and host your programs and apps online for free.
This is a quick and easy way to type in and run Clojure from a web browser. The "REPL" is "read, evaluate, print, loop": read some code, run it, print the result, and loop through the process until all the code is executed.

https://repl.it/languages/clojure

A Clojure babushka for the grey areas of Bash. Really, a Clojure interpreter as a native application with fast launch times. It is intended as a bash scripting replacement, but really is a (near) full release of Clojure as an interpreter. This also may be the easiest way to start learning Clojure. You only need a text editor and babashka. The normal Clojure tool chain has complexities and pecularities. The tooling around Clojure is (in some ways) harder to learn than the language.

https://github.com/borkdude/babashka


Introduction to clojure. Combine examples at this web page with repl.it above. learnxinyminutes.com has loads of other programming languages too.

https://learnxinyminutes.com/docs/clojure/


Clojure datomic ions repl remote

https://github.com/markbastian/replion

Learn clojure coding tutorial REPL examples Robert C. Martin (Uncle Bob)

http://blog.cleancoder.com/uncle-bob/2020/04/06/ALittleClojure.html

#### Programming languages

Stevan Andjelkovic argues that Erlang's inherent use of state machines allows application devs to concentrate on the application behavior. And that due to the nature of state machines, the application is very robust. This has been my experience with state machines, including the critter brains we used in the Island of Kesmai. Those non player characters relied on a state machine technology created by Kelton Flinn. 

https://github.com/stevana/armstrong-distributed-systems/blob/main/docs/erlang-is-not-about.md

Facts about State Machines. A nice, complete, synopsis of the beauty of state machines by Chris Pressey. Very cleverly addresses the concept of the "state" of the system by suggesting the term "mode". My favorite flavor of state machine is derived from what Kelton Flinn created for the Island of Kesmai, where state broadly included any aspect of the system that could be logically tested with an if statement. Calling that a mode seems to fit, and addresses confusion over state as a more narrow definition.

https://github.com/cpressey/Facts-about-State-Machines


PHP is probably the most horrible, poorly designed, bug ridden piece of crap in existence. I wish that were an exaggeration, but this quote from the excellent post below covers it: "Virtually every feature in PHP is broken somehow. The language, the framework, the ecosystem, are all just bad." Kudos to Evelyn Woods for this timeless analysis.

https://eev.ee/blog/2012/04/09/php-a-fractal-of-bad-design/


#### Education Career

First, Musk should do as he says and remove degree requirements from job descriptions and workplace culture. Second, there's a caveat to "smart guys don't need degrees". Really, those smart guys are just lucky. College (or not) wasn't the factor, just luck.

https://www.theguardian.com/technology/2020/mar/10/elon-musk-college-for-fun-not-learning


Ability to learn a spoken language correlates with programming better than math skills

Chantel S. Prat, Tara M. Madhyastha, Malayka J. Mottarella, Chu-Hsuan Kuo. Relating Natural Language Aptitude to Individual Differences in Learning Programming Languages. Scientific Reports, 2020; 10 (1) DOI: 10.1038/s41598-020-60661-8

https://www.sciencedaily.com/releases/2020/03/200302103735.htm

#### Operating Systems

Technical reasons to choose FreeBSD over GNU/Linux

https://unixsheikh.com/articles/technical-reasons-to-choose-freebsd-over-linux.html
