---
author: Cambatta
pubDatetime: 2024-05-24T01:22:00Z
modDatetime: 2024-05-24T01:22:00Z
title: Lyrics of Cambatta
slug: cambatta
featured: true
draft: false
tags:
  - lyrics
description: cambatta lyrics
---

In perhaps one of the strangest instances of multiple synchronicity I've ever experienced, in less than a year's time we had a spiritual experience that mirrored eachother's and I discovered a lesser known rapper (< 10,000 monthly listeners on spotify) from a blog I follow that posts nearly every hip-hop album release in real time. The album, LSD from 2020, caught my attention as strangely the lyrics mirrored so much of the spiritual elements of the expanded conceptual framework that existence now seemed to fit within. Far too much to be written off as coincidence, we listened again and again.

How could this be real? A question I find myself asking more than ever before over the past few years. There was more, on further inspection we discovered this artist had spent most of his adult life living in not only the same city, but the same neighborhood where we ended up finally finding a decent place to rent. And further, that he and his partner were also fighting a similarly soul-crushing civil case against the state as we were. At the same time.

Needless to say, these songs hold a particularly special place in our hearts now as they so mirror our experience over the years since 2020.

I wanted to see how well chatGPT would fare at writing a python script to scrape genius for lyrics given the link to an album as input.

I supplied ChatGPT with the following prompt, which really was not worded all that well. I could tell I was tired and could probably do better.

```
create a python script using beautifulsoup that takes a url as an argument,
it will download the content at the url and find all the links contained
within divs with a class of 'chart_row' , it will store these links
in an array and then loop through that array maintaining a counter variable
named iCounter initialized at a value of 1 and loading each link.
it will then scrape the content of these pages for divs with a class
containing the substring 'LyricsHeader__TitleContainer' and find the deepest
child node contained within that div storing the innerhtml of that node in a
variable named sTitle. it will also find the div with a class containing the
substring 'Lyrics__Container' and pull the  innerhtml of that div, stripping
all html from the content and storing it in a variable  name sLyrics.
once that is done the script will output the following markdown


### [value of iCounter] ) [value of sTitle]

[value of sLyrics]

Then it will increment iCounter and repeat for the next url in the array

```

This is the result. Yes it worked, first run:

```
#!/bin/python

import requests
from bs4 import BeautifulSoup
import re

def get_page_content(url):
    response = requests.get(url)
    response.raise_for_status()
    return response.content

def extract_links(url):
    content = get_page_content(url)
    soup = BeautifulSoup(content, 'html.parser')
    links = []
    for div in soup.find_all('div', class_='chart_row'):
        for a in div.find_all('a', href=True):
            links.append(a['href'])
    return links

def extract_title_and_lyrics(url):
    content = get_page_content(url)
    soup = BeautifulSoup(content, 'html.parser')

    # Extracting the title
    title_div = soup.find('div', class_=re.compile('LyricsHeader__TitleContainer'))
    sTitle = ""
    if title_div:
        deepest_node = title_div
        while len(deepest_node.find_all()) > 0:
            deepest_node = deepest_node.find_all()[0]
        sTitle = deepest_node.get_text(strip=True)

    # Extracting the lyrics
    lyrics_div = soup.find('div', class_=re.compile('Lyrics__Container'))
    sLyrics = ""
    if lyrics_div:
        sLyrics = lyrics_div.get_text(separator='\n', strip=False)

    return sTitle, sLyrics

def main(url):
    links = extract_links(url)
    iCounter = 1
    for link in links:
        sTitle, sLyrics = extract_title_and_lyrics(link)
        print(f"### {iCounter}) {sTitle}\n")
        print(f"{sLyrics}\n")
        iCounter += 1

if __name__ == "__main__":
    import sys
    if len(sys.argv) != 2:
        print("Usage: python script.py <url>")
        sys.exit(1)

    url = sys.argv[1]
    main(url)
```

## LSD: Lunar Solar Duality

### 1. Bloodmoon

[Cambatta]

For the past couple years I’ve seen tragedy at max<br/>
It’s getting dark I hope my shadow can adapt<br/>
Family home went from a palace to a shack<br/>
Dilapidated castle to a trap<br/>
Daddy never had me on his lap<br/>
So when a male authority figure at me I’m casually reacting with attack<br/>
I’ve always been this talented at rap<br/>
Only recently are niggas on me like I got a saddle on my back<br/>
Eve got her mouth on me like an apple in my sac<br/>
Fully automatic chopping how I’m hacking with the MAC<br/>
Mister robot with data I extract, trafficking the packs<br/>
On the block chain ain’t no tracking me on that<br/>
Travel back to Africa and back<br/>
With the artifacts, blueprints, papyrus and maps<br/>
I'm like Indiana Jones but if Harrison was Black<br/>
I’m just trying to keep my heritage intact<br/>
Electron, Effects on<br/>
Gen-etics long, 10x strong<br/>
Rocks wilder than Red Meth song, vest Teflon<br/>
Red Fez, sekmet spawn, techs get drawn<br/>
Slaughter pigs on this redneck farm<br/>
Wake them up with a Fed Ex bomb<br/>
Separate head, neck, arm, chest, legs gone<br/>
Body parts everywhere like on Sex Ed walls, medics called<br/>
World looking like the next red dawn<br/>
Smoke gas to the face like my head chevron it’s Cameron<br/>
Aleon, I’m beyond luck<br/>
Me on beyond Elon Musk<br/>
Me on beyond aeon flux<br/>
Breed all seed all queens I fucks<br/>
Evolving all thing I touch<br/>
Me on see-saw fling y’all up. up<br/>
See Mars, see stars, see stardust<br/>
See me in everybody, Murphy on Klump, yup<br/>
One Pac, Tupac, three Pac, none-chuck<br/>
Bruce Lee, Ali I punch, duck<br/>
Short arms can’t box with God<br/>
My arms long enough to beat god up if he got shrunk<br/>
LSDMT I puff out cloud that I be on<br/>
And pee on Trump<br/>
I’m the bully in the back of the retard bus<br/>
In front of a starving man I eat my lunch<br/>
Munch grey poupon, dijon brunch<br/>
So many slaves I don't need my thumbs<br/>
Press tab on tongue like a Reebok pump, jump<br/>
Jew man, jumanji on mush<br/>
John D. on dust, all this money I touch<br/>
It should read in me I trust<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
Bones of Osiris<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
​euphoria<br/>
Kendrick Lamar<br/>
[Nomxolisi Ndlangana]

Mother moon<br/>
Coat my throat with spirits that can only be found at the palms of dead legends<br/>
<br/>
That now live in the cosmos<br/>
For far too long we have buried our rites in this western plight to fly amongst stars<br/>
<br/>
And stand besides czars<br/>
At costs too high to land softly;<br/>
<br/>
We have forgotten we are luminous, rousing lunar gods under one God<br/>
We must go back, we must go back to get tomorrow right<br/>
Young man<br/>
<br/>
Light a match<br/>
<br/>
Start a fire and burn;<br/>
You are the sun my moonpie will soothe<br/>
<br/>
Abandon all biased system functions<br/>
And welcome to the introduction<br/>
An LSD induction<br/>
We are now at Cameron junction<br/>
This art serves as a spiritual function<br/>
Sun, son, son…<br/>

### 2. Bones of Osiris Lyrics

[Verse 1: Cambatta]<br/>
Solar-powered airplane<br/>
Following the daylight<br/>
Never have to say night<br/>
Never have to see dark<br/>
Hoping I can stay bright<br/>
Never ending theme park<br/>
Noah got the winged ark<br/>
Floating like a free hawk<br/>
Motion to the epoch<br/>
Quoting out the Enoch<br/>
Social with the griots<br/>
Yoga at the tea shop<br/>
Older than the Pequots<br/>
Soldier was the Ewoks<br/>
Vulcan at your weak spot<br/>
Open up the key locks<br/>
Kobe with the 3 shot<br/>
Postering a Divac<br/>
Holster when I need Glock<br/>
Bolting when I see cops<br/>
If I’m the animal who standing over me in green socks<br/>
Hopefully I meet Pac<br/>
Free not, everybody gotta pay to live<br/>
Laws were created by some racist pigs<br/>
You could never own a planet but he made it his<br/>
Then he stripped the languages from my Native lips<br/>
But I guess it’s just the way it is<br/>
If you make a man hungry he take greater risks<br/>
I would break into your crib just to raid your fridge<br/>
If I bear hug a bear I could break his ribs<br/>
I could never be a slave to this<br/>
Even though we on the plantation where satan lives<br/>
He don’t even got no clothes in his closet<br/>
Just fabric, a sewing machine and a little Asian kid<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
33<br/>
Cambatta<br/>
BloodMoon<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
[Chorus: Cambatta]<br/>
Bitch I'm bad to the bone<br/>
Bad to the motherfucking bone<br/>
Bitch I'm bad to the motherfucking bone<br/>
Bitch I'm bad to the bone<br/>
Never had a dad in my home<br/>
I got everything I have on my own<br/>
‘Cause I’m Black and I’m grown<br/>
And I’m bad to the bone<br/>
And I'm bad to the motherfucking bone<br/>
Bitch I’m bad to the bone<br/>
Never had a dad in my home<br/>
I got everything I have on my own<br/>
<br/>
[Verse 2: Cambatta]<br/>
Shepherd of the lambs and they all Gini<br/>
Attached to the bottle like a lost genie<br/>
Fly like a seagull in a beanie<br/>
I can feel it in the air like a Lear’ as I soared freely<br/>
Can the Lord see me<br/>
If my eyes are windshields to my soul my song is long squeegee<br/>
Beyond 3D, psychic went blind trying to palm read me<br/>
Jack you in public you all Peewee<br/>
I'm a addict but I'm functional<br/>
A habit's only bad if you ain't punctual<br/>
Only in the midst of chaos am I comfortable<br/>
Religion works ‘cause human beings are gullible<br/>
Talking business, have a brunch with you<br/>
Talking metaphysics, smoke a blunt with you<br/>
Talking to some women, I'ma fuck a few<br/>
But if you talk about my mama then I'm snuffing you<br/>
I hear the beat and I just mumble through<br/>
I'm mumbling now I'm just eloquent as Huxtables<br/>
If you're not as smart as me I’m dumb to you<br/>
My favorite color's the number W<br/>
I’ll never call another man a boss<br/>
Rocks are only hard ‘cause your hands are soft<br/>
Never had a father or a Santa Claus<br/>
If I see a reindeer I’ll rip his antlers off<br/>
[Chorus: Cambatta]<br/>
Bitch I'm bad to the bone<br/>
Bad to the motherfucking bone<br/>
Bitch I'm bad to the motherfucking bone<br/>
Bitch I'm bad to the bone<br/>
Never had a dad in my home<br/>
I got everything I have on my own<br/>
‘Cause I’m Black and I’m grown<br/>
And I’m bad to the bone<br/>
And I'm bad to the motherfucking bone<br/>
Bitch I’m bad to the bone<br/>
Never had a dad in my home<br/>
I got everything I have on my own

### 3) 33

[Kenny Buttons]<br/>
Lay your head, no worries<br/>
Time will come<br/>
Life is a gamble, playing what it dealt though<br/>
I been down plenty but I’m up and stay ready ain’t much I can’t handle<br/>
Devil on my ass he keep trying to suck me up, take my life<br/>
God done pulled me from the depths of this hell too many times<br/>
<br/>
[Cambatta]<br/>
Around the age of 5 was the very last time<br/>
I looked my father in the eyes before the nigga bounced<br/>
I was bout 6 when I seen my momma get her wig split<br/>
By some nigga she let in the house<br/>
I was 7 when I learned my first lesson bout sexing<br/>
From the magazine collection underneath the couch<br/>
I was 8 when I learned about base<br/>
It was Christmas I was looking for my presents and I found an ounce<br/>
I was 9 when I shot my first 9 in the backyard with my uncle John<br/>
Them was good times<br/>
I was 10 when I lost my best friend to a stray bullet<br/>
That I heard was fired out that same 9<br/>
11 when I learned about heaven from the reverend<br/>
When he told me that was where my homie probably was<br/>
I was 12 when I learned about hell<br/>
Momma wasn't doing well, whole fam on a lot of drugs<br/>
13 I was smoking so much weed, I was basically a fiend<br/>
I was high as fuck everyday<br/>
14 I was on the sports team<br/>
But I quit it cuz I knew I wasn't going to the NBA<br/>
15 got pussy for the first time<br/>
And getting more pussy's only thing up on a nigga mind<br/>
16 started writing 16's niggas said I spit mean<br/>
Bitches love it when a nigga rhyme<br/>
17 I ain't graduate but a nigga needed money<br/>
I was on the corner trying to slang trees<br/>
18 graduated to the base fiends<br/>
Now I'm on to big money and great things<br/>
New whip on 18's, new chick, my chain swing<br/>
Caught up in the gang thing, trying to make my name ring<br/>
Even put a mask on, I let that AK ring<br/>
By the age of 19 I'm in sitting in that state bing<br/>
Sing<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
NXggXr chrXst<br/>
Cambatta<br/>
Bones of Osiris<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
[Kenny Buttons]<br/>
Lay your head, no worries<br/>
Time will come<br/>
Those who’ve sinned against you<br/>
Soon will fall<br/>
<br/>
[Cambatta]<br/>
I ain't get released til I was 21<br/>
Turned me to a monster I am no longer my mother's son<br/>
By the age of 22 I had my first child I ain't raising<br/>
Now my mother got another son<br/>
I was 23 when my uncle called me<br/>
And told me that my father died, but I ain't cry<br/>
24 I was sniffing so much caine, I was smoking so much dust<br/>
All I thought about was homicide<br/>
25 I was sitting in the ER<br/>
I caught a shot from the kid that I robbed when I was 18<br/>
26 got addicted to the pills that the doctor gave me<br/>
I was struggling to stay clean<br/>
27 learned my lesson, I was back inside corrections<br/>
But I think it was a blessing in disguise though<br/>
Turned Christian for a second, then Islamic, met the brethren<br/>
But I had a lot of questions on my mind though<br/>
That religion couldn't answer started reading every book that I could find<br/>
I'm getting smarter as my time goes<br/>
I was getting so much wiser, I could feel my soul is rising<br/>
I can finally look myself in the eyes though<br/>
Finally got paroled at 31<br/>
Trying to make connections with my son but he don't know me<br/>
He remind me of the old me when my father left me lonely<br/>
So I started as his homie<br/>
Schooled him to the lessons life showed me hoping later he'll console me<br/>
When he see me as a man and not a phoney<br/>
32 I turned a new leaf<br/>
My new queen pregnant she 32 weeks<br/>
My son is living with me and his mother we speak<br/>
I helped her get off drugs, clean 32 weeks<br/>
Started up a program for the brothers in the streets<br/>
It's an outreach, free them with the knowledge we teach<br/>
Turning water into Henny<br/>
Everybody at the table getting bread and we eat<br/>
When they see you as a king<br/>
Just be aware of all the envy and the jealousy it brings<br/>
Especially your team, it's usually the one that comes in second<br/>
That develops a deceptive way of being<br/>
Left hand man he set me up<br/>
Went and talked to the forces and wet me up<br/>
Finally they murdered me at 33<br/>
Nigga Christ you heard of me

### 4) NXggXr chrXst Lyrics

[Verse 1: Cambatta]<br/>
I'm back from the death, I don't have to repent, I don't ask for the breath<br/>
Life is of gradual steps and I feel like the last one is next<br/>
But they knock me down, a nigga just a king without a crown<br/>
I'm so hungry I don't need to speak I let my stomach growl, you just wonder how<br/>
Melanin lord, the sun is my energy source, the one that the devil informs<br/>
My head full of thorns, I'm stuck in this twenty first century war<br/>
Lucidly thinking, lucy the juice that I'm drinking, hallucinate truth and its meaning<br/>
I view what computers are dreaming, unusual humanoid heathen<br/>
Delusional even, at funerals chiefin’ I laugh in a room full of grievance<br/>
My hugest achievement is proving that music is fluent as breathing<br/>
<br/>
[Chorus: Cambatta]<br/>
I give them life<br/>
I give them life<br/>
From the dark, I give them light<br/>
Nigga Christ x2<br/>
<br/>
[Verse 2: Cambatta]<br/>
My body is cybernetic, oxygen is a psychedelic<br/>
Make it move kind of like kinetics, make the coke hard like I'm it's fetish<br/>
Now my wifey jealous<br/>
Ghetto sophistication in my mental configuration<br/>
Pissing yellow precipitation on your head while I'm in a spaceship<br/>
‘Til I'm feeling weightless<br/>
Higher learning got me sipping Remy, shooting banks up ‘cause a rapper poor<br/>
I'll be at your door with a MAC or more like the cracker rapper or the Apple store<br/>
You would think I'm Cinderella's prince<br/>
‘cause I'm going door to door with the pump<br/>
If the shoe fits let it ring, street sweeper like a broom so you better jump<br/>
Jump off with the tramp on lean, plus two, that's a triple tuck<br/>
Grip a pump, it's a UFO with a laser beam that'll lift him up, up, up<br/>
Alienate you, you gonna think that an alien ate you<br/>
Eat you so fast that I barely can taste you<br/>
I can see you scared, the fear in your facial<br/>
Thank you<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
Sun of Whorus<br/>
Cambatta<br/>
33<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
[Chorus: Cambatta]<br/>
I give them life<br/>
I give them life<br/>
From the dark, I give them light<br/>
Nigga Christ x2<br/>
<br/>
[Verse 3: Cambatta]<br/>
I turn vices to virtues, call it eyelid reversal, I wake up your light and resurge you<br/>
I restore the sight in your third view my science is verbal<br/>
From deep in the silence I birth you, circle divided by circle<br/>
Inside of a cypher of circles like vesica piscis I merge you, the cycles converge you<br/>
When God used his joystick to guide me<br/>
He played so hard that he numbed his thumbs<br/>
I'ma hit a lick like I punched a tongue, I'm as sharp as the knife Jay stuck in Un<br/>
Crew iller I'm the hundred one, I got hungry lungs<br/>
Me versus the whole world's population still feels like a one on one<br/>
You see impossible, I see I'm possible, momma look at what I can do<br/>
Body the obstacles, Batta Muhammad the Honorable<br/>
Khalid Muhammad on Donahue<br/>
<br/>
[Chorus: Cambatta]<br/>
I give them life<br/>
I give them life<br/>
From the dark, I give them light<br/>
Nigga Christ x2

### 5)Sun of Whorus

Hood nigga, crack baby, ghetto lord<br/>
Magneto, I can show you what the metal's for<br/>
General, got recruited for the devil's war<br/>
Cross niggas, slam on them, then I score<br/>
Hell welcomed me, heard that heaven got a metal door<br/>
Never sleep, cuz when I dream I see death galore<br/>
Goat god, it's not an acronym or metaphor<br/>
Ram god, how a human got a head of horns<br/>
Metal rain, you should probably check the weather more<br/>
Hot lead will poor<br/>
Check his pulse, yeah that nigga's dead for sure<br/>
Bet he get resurrected in the belly of pregnant whore<br/>
<br/>
<br/>
Smell fear, and it stinks in here<br/>
Smells like hot pork when police are scared, yeah<br/>
Every time I kill a bear I'ma eat the bear, yeah<br/>
Smell fear, nose pick I'ma feast in here<br/>
Fe fi fo fum, the beast appear, yeah<br/>
See blind, no sun for at least a year, what<br/>
Fe fi fo fum and the beast appear, yeah<br/>
See blind, no sun for at least a year, what<br/>
<br/>
Hood nigga, crack baby, ghetto lord<br/>
Good kids turn bad when they get ignored<br/>
Dear dad, you created me but I was never yours<br/>
I'm a king, put a sword in a stone I'ma get the sword<br/>
Got the keys, olly olly oxen free<br/>
The cops on me, squally watching on the block for me<br/>
I got the trees, molly, oxy and I got the E<br/>
Them thots on me, mami wanna give the twat to me<br/>
Probably walking with a Glock on me\*\*\*<br/>
Snapshot, got a cannon on me like photography<br/>
Zoom in but you can't catch me, right handed but I play lefty<br/>
Wayne Gretsky, give me 8 Espy's, snort coke cuz I hate Pepsi<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
Fall of Feinix<br/>
Cambatta<br/>
NXggXr chrXst<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
Smell fear, and it stinks in here<br/>
Smells like hot pork when police are scared, yeah<br/>
Every time I kill a bear I'ma eat the bear, yeah<br/>
Smell fear, nose pick I'ma feast in here<br/>
Fe fi fo fum, the beast appear, yeah<br/>
See blind, no sun for at least a year, what<br/>
Fe fi fo fum and the beast appear, yeah<br/>
See blind, no sun for at least a year, what

### 6) Fall of Feinix Lyrics

No sleep, no dreams<br/>
From a coke fiend to dope fiend<br/>
From crack baby to crack fiend to blow speed<br/>
Nose bleed, can't wear the shirt if there's no sleeves<br/>
If I overdose and I die I don't gotta go clean<br/>
Numb it so I don't gotta feel it again by no means<br/>
The lens on my black spectacles<br/>
It's nebulous, resembling stems with the crack residue<br/>
Specimen, testing the lab chemicals<br/>
Past schedule, down to my last fentanyl<br/>
Free city SNAP medical, that destitute<br/>
Physician written scripts chicken scratch legible<br/>
Get a pack sell a few, do them all buy them back<br/>
Family thinks I'm on crack, why is that?<br/>
It's cuz I go to drugs when this life attacks<br/>
As it's getting harder, me getting high is how I react<br/>
Sleepwalk through this prolonged suicidal nap<br/>
Anywhere I lay is potentially where I'm dying at<br/>
Relapse every time I hear a striking match<br/>
Cuz I never know where my lighter's at<br/>
Sleeping with the roaches and the giant rats<br/>
Addict since my grammy gave me grape flavored Dimetapp, I was smacked<br/>
Keep slipping, keep sliding back<br/>
I need a map just to find a map<br/>
Walking validation of all the stereotypes of blacks<br/>
I'm a nigga and I'm fine with that<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
Scale of Anubis<br/>
Cambatta<br/>
Sun of Whorus<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
<br/>
<br/>
The crack baby is grown now<br/>
Still a lone child, suffocating in a smoke cloud<br/>
Put the coke down, whole town on the dope now<br/>
Put the coke down, whole town on the dope now<br/>
I got addiction in my blood and it shows now<br/>
Heart is weak, deviated septum in my nose now<br/>
Put the coke down, whole town on the dope now<br/>
Put the coke down, whole town on the dope now<br/>
They say that everything that comes around goes 'round<br/>
All them dealers selling to my momma on the dope now<br/>
Put the coke down, whole town on the dope now<br/>
Put the coke down, whole town on the dope now<br/>
<br/>
<br/>
<br/>
My spirit animal is a cold turkey<br/>
Body made of water but it's so murky<br/>
Dirty, name Flint when this hoe slurps me<br/>
She don't like me she just coke thirsty<br/>
Trying to get that brain freeze like a cold slurpy<br/>
Shirley, she look 50 in her low 30's<br/>
In high school she was so curvy<br/>
Used to curve me, karma has no mercy<br/>
My drug abuse history is so deep<br/>
In order for a copper to frisk me he gotta soul search me<br/>
See police and turn white like Jerome Kersey's home jersey<br/>
Mumbling in court like a stoned Furby<br/>
I'm trying to walk but it's so blurry<br/>
Don't worry I'm in no hurry<br/>
My emotional aptitude is rather shrewd<br/>
My inclination for discernment is null and void<br/>
Hugging me is redundant as punching rubber boy<br/>
Once upon a time I was mother's joy, now I'm just a droid<br/>
Numb to love, I've become annoyed by everybody's voice<br/>
Any sympathetic expression is but a muffled noise<br/>
So lethargic everything I do is hypothetic<br/>
High and pathetic, diet is diabetic<br/>
Stress levels defy the methods of Dianetics<br/>
Lord Xenu couldn't clear me with a science lesson<br/>
I'm not excited by the liar trying to find the heaven<br/>
I'm just trying to find the exit, quite pretentious<br/>
Lost child to whom life rejected<br/>
Stuck stifled through this time regression, everything's a suicidal weapon<br/>
I got anxiety and hyper tension<br/>
Hoping that the doctor can give me xannies for my depression<br/>
I think I need some oxys cuz my spine is tensing<br/>
Plus I'm out of methadone, they got me fighting medics<br/>
Twin nostrils hit blow like it's 9/11<br/>
I'm a nigga and I'd like to mention<br/>
If I overdose and I die I don't gotta go clean<br/>
Numb it so I don't gotta feel it again by no means<br/>
<br/>
The crack baby is grown now<br/>
Still a lone child, suffocating in a smoke cloud<br/>
Put the coke down, whole town on the dope now<br/>
Put the coke down, whole town on the dope now<br/>
I got addiction in my blood and it shows now<br/>
Heart is weak, deviated septum in my nose now<br/>
Put the coke down, whole town on the dope now<br/>
Put the coke down, whole town on the dope now<br/>
They say that everything that comes around goes 'round<br/>
All them dealers selling to my momma on the dope now<br/>

### 7) Scale of Anubis Lyrics

[Cambatta]<br/>
I just smoked all my money up and I'm still hurting<br/>
Up until the day my grammy died she was still working<br/>
I can count on my hands how many times I’ve met a real person<br/>
Blew the engine out before I even got the wheels turning<br/>
Still yearning, my passion's becoming a real burden<br/>
Still learning, though I know who death is, I be still flirting<br/>
Reveal curtain, think I test her just to feel certain<br/>
So when It's destined I don't feel nervous<br/>
Guess the question's what is real purpose?<br/>
<br/>
<br/>
<br/>
If God made me in his image, then he must've been a nigga too<br/>
Broke and hungry with no dinner too, getting tempted by these women too<br/>
If God made me in his image, then he must've been a sinner too<br/>
Grew the apple that she bit into<br/>
<br/>
<br/>
<br/>
[Natural Onyx]<br/>
First episode, I just want to talk about what's on my mind<br/>
Before I explode, staring at these four walls got me so confined<br/>
And I'm uneased<br/>
Sipping on antifreeze, yeah<br/>
Everyone knows, I'm about one, two, three steps from the line<br/>
Out of control, I don't really mean to be this damn unkind<br/>
But I'm uneased<br/>
Sipping on antifreeze, yeah<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
NuMirrorcal<br/>
Cambatta<br/>
Fall of Feinix<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
<br/>
<br/>
[Cambatta]<br/>
I guess I wish I knew how gravity felt<br/>
Cuz either my head in the clouds or I'm getting mad at myself<br/>
God listened but my pride wouldn't let me ask him for help<br/>
It's like my spirit got a chastity belt, I put my broken heart back on the shelf<br/>
<br/>
God is not to blame<br/>
You are not to blame, daddy's not to blame<br/>
Mommy's not to blame<br/>
Devil's not to blame, karma's not to blame<br/>
Batta's not to blame<br/>
They try to tell me that we are all the same<br/>
But the thing that makes you you and me me are not the same<br/>
<br/>
<br/>
<br/>
If God made me in his image, then he must've been a nigga too<br/>
Broke and hungry with no dinner too, getting tempted by these women too<br/>
If God made me in his image, then he must've been a sinner too<br/>
Grew the apple that she bit into<br/>
<br/>
<br/>
<br/>
[Natural Onyx]<br/>
First episode, I just want to talk about what's on my mind<br/>
Before I explode, staring at these four walls got me so confined<br/>
And I'm uneased<br/>
Sipping on antifreeze, yeah<br/>
Everyone knows, I'm about one, two, three steps from the line<br/>
Out of control, I don't really mean to be this damn unkind<br/>
But I'm uneased<br/>
Sipping on antifreeze, yeah

### 8) NuMirrorcal Lyrics

Would you die for something that you'd rather be alive for?<br/>
Is it something true enough to lie for?<br/>
Father I'm the you that you deny yours<br/>
Why was I born?<br/>
I survive for shit that you would do a suicide for<br/>
Got a momma I would do a homicide for<br/>
All this crying got a nigga eyes sore, tell me why Lord?<br/>
All this praying but you don't reply Lord<br/>
Can you send me down a sign Lord<br/>
Got a nigga kneeling down on my floor<br/>
Sun rose got the spike thorns like what Christ wore<br/>
Floating like a ribbon in a sky war, this is my story<br/>
Like a life force you would die for, for divine glory<br/>
Can you help me God cuz I'm falling<br/>
Can you hear me God cuz I'm calling<br/>
This is my story<br/>
<br/>
Got some shit I need to say<br/>
Lord I hope you hear me when I pray<br/>
It ain't good around my way<br/>
Lord I need a miracle today<br/>
<br/>
Today<br/>
<br/>
Got some shit I need to say<br/>
(I need a miracle, I need a miracle)<br/>
Lord I hope you hear me when I pray<br/>
(I need a miracle, I need a miracle)<br/>
It ain't good around my way<br/>
(I need a miracle, I need a miracle)<br/>
Lord I need a miracle today<br/>
(I need a miracle, I need a miracle)<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
24ours (Day & Night)<br/>
Cambatta<br/>
Scale of Anubis<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
Today<br/>
<br/>
Need a little help, I can't do it by myself<br/>
All I got is me, I don't got nobody else<br/>
Traded in my time, family and health<br/>
Have you ever felt like you hot enough to freeze<br/>
But you cold enough to melt<br/>
Feeling like a waste, should be hanging from a belt<br/>
Got a soul and it's for sale<br/>
Is it only for the wealth?<br/>
Am I talking to myself?<br/>
On a knee I never knelt<br/>
Got me pleading for your help, gotta play the way it's dealt<br/>
<br/>
Got some shit I need to say<br/>
Lord I hope you hear me when I pray<br/>
It ain't good around my way<br/>
Lord I need a miracle today<br/>
Today<br/>
Got some shit I need to say<br/>
(I need a miracle, I need a miracle)<br/>
Lord I hope you hear me when I pray<br/>
(I need a miracle, I need a miracle)<br/>
It ain't good around my way<br/>
(I need a miracle, I need a miracle)<br/>
Lord I need a miracle today<br/>
(I need a miracle, I need a miracle)<br/>
Today<br/>
I've been fighting for my life, I've been fighting for the right to see the light

### 9) 24ours (Day & Night) Lyrics

[Intro: Cambatta]<br/>
All I got is 24 hours<br/>
(Wait, wait, wait, wait)<br/>
(All a nigga' got)<br/>
Look<br/>
(That's all a nigga' got, all a nigga' got)<br/>
<br/>
[Verse 1: Cambatta]<br/>
All I got is 24 hours (yeah)<br/>
Live and die in 24 hours (lord)<br/>
What is really age but the same day<br/>
Looping in a phase of just 24 hours? (what)<br/>
If your neighbor does more with the same 24<br/>
Got to ask yourself: what is your power? (God)<br/>
Are you living for the struggle or honor? (yeah)<br/>
Shit'll make a nigga summon forefathers (Yah)<br/>
I’m just thankful that my mother brought Batta<br/>
Should've brung a double dozen more flowers<br/>
Uppers or downers, blunt of pure sour<br/>
Smoking through my last 24 hours<br/>
Same sun and moon tug of war drama<br/>
Feel the tears, look above and saw showers<br/>
I just wish I had a hundred more hours<br/>
God's generous, but 24's modest<br/>
What we got a budget for<br/>
Can I borrow some of yours?<br/>
Spend it quick as 24 dollars<br/>
Gone faster than my mother's warm chowder<br/>
I can feel the tender loving pure power<br/>
His 24, her 24, their 24 - which 24's ours?<br/>
Would you trade your money for hours?<br/>
Or trade your hours for a couple more commas?<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
NXggXria tXsla<br/>
Cambatta<br/>
NuMirrorcal<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
[Chorus: Cambatta]<br/>
First you see the dark and then you see the light<br/>
Then you see the day and then you see the night<br/>
I'm just narrating what I see inside<br/>
Thanking my creator I can read and write<br/>
Stumbled on my path I think I need a ride<br/>
Struggling and sadness bring my evil side<br/>
Swallowing my ego and I eat my pride<br/>
Fighting till the end until I see the prize<br/>
<br/>
[Verse 2: Cambatta]<br/>
All I got is day and night...<br/>
...Right?<br/>
Night is dark, day is light<br/>
I say good morning, then I say goodnight<br/>
Day and night<br/>
My only options in the game of life<br/>
Play the dice<br/>
You'll lose them both if you don’t pay the price<br/>
Night is black, and day is white<br/>
Kind of racial, right?<br/>
Sundial is made of ice like a glacier might<br/>
Calibrated the way I like<br/>
Count to 24 hour hand<br/>
Rotate it twice<br/>
Day'll change to night<br/>
Mother Nature, and Father Time<br/>
Had a baby and they named it Christ<br/>
They' only son, I hope they raise him right<br/>
Daughter, too - her name is Luna but they ain't alike<br/>
When son is down, you see her rising to her greatest height<br/>
Feel like E.T. on his flying levitating bike<br/>
You'll see my shadow on the moon 'cause I was taking flight<br/>
Living like I’m made to shine (yeah)<br/>
[Chorus: Cambatta]<br/>
First you see the dark and then you see the light<br/>
Then you see the day and then you see the night<br/>
I'm just narrating what I see inside<br/>
Thanking my creator I can read and write<br/>
Stumbled on my path I think I need a ride<br/>
Struggling and sadness bring my evil side<br/>
Swallowing my ego and I eat my pride<br/>
Fighting till the end until I see the prize<br/>
<br/>
[Verse 3: Red Pillar]<br/>
I'll be mad if you ain't at my wake<br/>
In a Wraith blasting Faith and some Pastor Mase<br/>
Throwing bricks wrapped in mask and tape<br/>
Take me from the 5th down to Astor Place<br/>
Let me see the grin on the bastard's face<br/>
I'm coming from the kin of the master race<br/>
Next to Nipsey in the master's race<br/>
I know the code, so I cracked the safe<br/>
Bury me with Sebi in his casket late<br/>
And we' owners so our master's safe<br/>
Bury me in polo with a gat on waist<br/>
Victory is sweet I need the aftertaste<br/>
<br/>
[Chorus: Cambatta]<br/>
First you see the dark and then you see the light<br/>
Then you see the day and then you see the night<br/>
I'm just narrating what I see inside<br/>
Thanking my creator I can read and write<br/>
Stumbled on my path I think I need a ride<br/>
Struggling and sadness bring my evil side<br/>
Swallowing my ego and I eat my pride<br/>
Fighting till the end until I see the prize

### 10) NXggXria tXsla

[Cambatta]<br/>
Black Tesla, first name Niggerla<br/>
Wizardous, gifted magician you get to live amongst<br/>
They say indigenous knowledge is from the visitors\*\*\*<br/>
When really we just tapping in algorithms from within us<br/>
Hidden from getting clutched by the wicked ones<br/>
I'm the only physician it's not forbidden from<br/>
Paulo Coelho's literature's living syllabus<br/>
It's synchronous, I sit on the treasure before I dig it up<br/>
Writing til my back hunched over like Spina Bifida<br/>
Calligrapher, when writing Leviticus I was in a rush<br/>
Feel epiphanies tickling in my viscera<br/>
Mythical cinema with nonfiction insignia<br/>
I'll invent an artificial brain<br/>
So close to mine it's arguably the same<br/>
I'll invent a sound modulator that can stop it when it rains<br/>
And a magnet that can shift how astronomy's arranged<br/>
The other day while getting high on the couch<br/>
I invented a water filter that takes hydrogen out<br/>
The CIA surrounded every side of my house<br/>
They heard I got the hidden secrets to what life is about<br/>
I'ma gather all the brightest mechanical engineers<br/>
And convince them to build me a super telescope<br/>
With this telescope I can debunk<br/>
Every astronomical ideology ever spoke<br/>
Nasa wanna peak, I'ma tell them nope<br/>
Space X wanna look, I'ma send them quotes<br/>
Free viewing for the woke and ascended folks<br/>
Rewrite every science book ever wrote<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
Grand Number TheoRam (GNT 1:1)<br/>
Cambatta<br/>
24ours (Day & Night)<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
Black Niggerla Tesla<br/>
Greatest of the non-living living inventors<br/>
Thomas Edison was just a wicked embezzler<br/>
And Benjamin Franklin's a sick kiddie molester<br/>
They call me Niggerla Tesla<br/>
Never am I witnessed in a physical venture<br/>
Only as a hologram in digital lectures<br/>
But even when you hidden the reptilians catch ya<br/>
<br/>
Pocket knife crafted with Damascus steel<br/>
Watch easily I skin a gator like an apple peel<br/>
My IQ would lead you to believe<br/>
That my daddy used to microdose acid in my happy meal<br/>
Light blunts with the fire that be blasting out the back of a Batmobile<br/>
I actually have for real<br/>
I'm currently blueprinting a watch<br/>
That does more than just ticking and tocks<br/>
It creates a forcefield that's resistant to the pistol and Glocks<br/>
You can safely talk shit to the cops, I giggle at shots<br/>
I'll invent a form of corn on the cob<br/>
So you'll never need more than you got<br/>
Swallow kernels whole, shit them out, stick them right back on the cob<br/>
Rinse it off, having one is an unlimited crop<br/>
You better give me my props<br/>
I might be the most innovative nigga we got<br/>
I can hand carve a whistle from rock<br/>
That can make a sound in a pitch that can lift up a yacht<br/>
The fabric in my new cloth can wipe the soles of your shoes off<br/>
And make them smooth enough that anyone can moonwalk<br/>
Just had a new thought, never seen a pig fly<br/>
I should put cybertronic wings on a huge hog<br/>
Tell your wife I got a tampon that vibrates<br/>
I'll make a bottle of wine from one dry grape<br/>
My iPhone battery lasts nine days<br/>
I see music in tetrahedrons and sine waves<br/>
I use words as joysticks for mind games<br/>
My spirit is so much older than my brain<br/>
Best invention since record players<br/>
It's called a quantum synthetic voice replicator<br/>
Speech emulator, this ain't even me speaking<br/>
But I'm synthesized so well that I was never greater<br/>
I coded it as a seventh grader<br/>
The prototype was designed with the same tech as Vader's<br/>
Creativity is second nature<br/>
I used to blow up shit in my yard and upset the neighbors<br/>
Experiments in the basement and held the deadly vapors<br/>
Solar's easy, made a lunar electric generator<br/>
Mom asked God for a prophet when she said her prayers<br/>
She was pregnant seven seconds later<br/>
She named me Niggerla Tesla<br/>
My theorems give the sharpest mathematicians dementia<br/>
I see reality before the image can render<br/>
Squinting my retina, vision bigger than Kepler's<br/>
<br/>
They call me Niggerla Tesla<br/>
The biggest ideas need an even bigger investor<br/>
My current fee is set at a billion dollars an hour for encrypted voice chat<br/>
Each additional minute is extra<br/>
<br/>
The name's Niggerla Tesla<br/>
My newest device drops next middle December<br/>
Presenting you a pain-free midget extender<br/>
Make a fat dwarf tall, skinny and slender<br/>
<br/>
When I'm whipping a Tesla<br/>
Multiple rhymes, I'm a twelve syllable stretcher<br/>
Ghost in my mind like a self inner Alexa<br/>
Woke up inside cyber realms mythical sectors<br/>
<br/>
Not your typical Tesla<br/>
Put a rocket engine on a miniature Vespa<br/>
Digit collector, rare critter protector<br/>
The beetle key is the levitation gift of the Khepera<br/>
<br/>
[Songbird]<br/>
(Reality is)<br/>
The earth is yours so don’t let your inner power unfold<br/>
(Reality is)<br/>
The only real access we have is our own minds<br/>
(Reality is)<br/>
It’s more than energy<br/>
(Reality inside)<br/>
Inside this physicality<br/>
(Reality is)<br/>
Now that you’re waking up we’re here to let you know it’s your time<br/>
(Reality is)<br/>
We made everything<br/>
(Reality inside)<br/>
All around us

### 11) Grand Number TheoRam (GNT 1:1)

Most loners are alone I feel all one<br/>
Not half of one, the whole where the half is from<br/>
A hole is but a circle which is actually none<br/>
I'll go back to one before two<br/>
4, 2 forty two, fortitude, add them then it's 6<br/>
6 atoms, 4 and 2 is 8<br/>
Infinity when vertical, Zer O with a twist<br/>
Like a torus or a Möbius strip<br/>
It's the holy of the of the holier glyphs<br/>
Number 9 is a 1 with his nose on his dick<br/>
Number 2 is synonymous with more than just shit<br/>
<br/>
Do-du-ality when the polar is split<br/>
Cross sun's your solar eclipse<br/>
Devil ate teens that know the 3 six<br/>
Deep thesis<br/>
The Zero is a egg<br/>
With the capacity of hatching to any fraction imagined In your brain<br/>
<br/>
I'm doing numbers<br/>
I'm doing numbers<br/>
I'm doing number<br/>
My mathematics are forcing you to wonder<br/>
<br/>
Number 1 is depicted with a straight line<br/>
The quickest way to travel within space time<br/>
Number 2 is a 1 on his knee praying<br/>
To itself 1's a capital I<br/>
Number 3 is like an open set of hand cuffs<br/>
Trial tried him 8 when clamped up<br/>
Upper case Q is a zero when it's pissing<br/>
Lower case q is a 9 when it stands up<br/>
Letters are just numbers, and words are like algebra formulas<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
Mic El JahXsun<br/>
Cambatta<br/>
NXggXria tXsla<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
That your brain processes to makes colors<br/>
Atoms are just pixels<br/>
<br/>
And DNA's coding that's activated by light and then crystallizes within you<br/>
<br/>
64 codons<br/>
6 plus 4 like the bits in my 'tendo I play Mario on<br/>
10 said 1 marry O<br/>
New miracles, 11's 1 in the mirror though<br/>
Merry go round like the sun do<br/>
Time starts with a 1, ends with a 1 too<br/>
Or 12 slowed down<br/>
Toooo wealth's what I run to<br/>
Fore word, like the word fore, the hole in 1...2<br/>
Like 3 4's, number of disciples of the king lord<br/>
Figures that I bring forth<br/>
5 like the points in the pentagram<br/>
You flip it the image is goat-headed man<br/>
Baphomet supreme 5 power yes<br/>
The balance between Ra and Set<br/>
Ra set, reset god in flesh<br/>
5 letters when allah is text<br/>
5 fingers 5 toes and they all in set<br/>
Like 2 arms 2 legs head star when they all are stretched<br/>
I guess you can say I'm obsessed<br/>
Counting down to my conscious death, bless<br/>
<br/>
I'm doing numbers<br/>
I'm doing numbers<br/>
I'm doing number<br/>
My mathematics are forcing you to wonder<br/>
<br/>
<br/>
<br/>
When I think about what numbers are<br/>
My brain gets numb bizarre<br/>
One solo SOL, Latin for sun and star<br/>
The sum of your birth numbers is what you are<br/>
My social security is a vin number<br/>
My body is a running car...bon based organism<br/>
My dimension is the 4th edition<br/>
At 4:44 I be portal shifting<br/>
I measure time with the silence before the ticking<br/>
I'm the first before the second before the minute<br/>
You don't get it when I fidget with these digits<br/>
I'm too cold with numb burrs, frigid<br/>
Numb birth labor with the painkillers<br/>
I'm a priest scripting, listen<br/>
Six is Sex<br/>
Six is legs which insects steps<br/>
Sick like incest sin<br/>
Inception of the sixth sense in since six sensations<br/>
Scarred like a sensei shin<br/>
3rd rock finished only six days in<br/>
Rested on the 7th like a sick day in<br/>
In Days Inn room I predict they sin<br/>
A little acid out the big basin<br/>
I took the trip that shift majins<br/>
You see Z, I see 2 7's<br/>
A triangle's a 7 in reflection<br/>
According to my middle school calculator<br/>
Seven million, seven hundred thirty four thousand<br/>
Two hundred and six people will go to hell<br/>
Whoever coded this reality wrote it well<br/>
1 is a phallus, 0 is a yoni<br/>
They made 8 kids and the family is growing<br/>
<br/>
<br/>
I'm doing numbers<br/>
I'm doing numbers<br/>
I'm doing number<br/>
My mathematics are forcing you to wonder

### 12) Mic El JahXsun Lyrics

[Verse 1: Cambatta]<br/>
My name is Michael Jackson, perfect mix of white and black skin<br/>
Nose carved by the finest craftsmen<br/>
Moonwalk across ice in Aspen, modern Christ of Nazareth<br/>
Beyond anything the mind imagined<br/>
I look like Michael Jackson, golden shoulder pads on shiny jackets<br/>
Diamond Breitling blinding when the lights are flashing<br/>
Wild fashion matching, back when 'Member the Time was platinum<br/>
Like Aladdin when his wife is Jasmine<br/>
She look like Michael Jackson<br/>
Are these bones in my face or some type of plastic?<br/>
I named my son Blanket, cuz when he was born<br/>
That's what he was tightly wrapped in<br/>
Stories never ending I feel like Sebastian<br/>
But more like Michael Jackson<br/>
Man's body that a child's trapped in, instead of playing it's most likely practice<br/>
Joseph hit me with a violent thrashing, work us like we addicts<br/>
Spirit stifled stagnant, daddy I ain't faggot<br/>
I give a kid a hug, people think I'm trying to grab him<br/>
Call it pedophile's actions, but I'm just Michael Jackson<br/>
<br/>
[Verse 2: Cambatta]<br/>
Asexual, inside retracted<br/>
Suppressed libido shifts the high mind synaptics<br/>
Space time collapses spinning like a cyclone<br/>
Twisting like a spiral traveling, til I'm not spinning<br/>
Like a dreidel to a righteous Catholic<br/>
Jehovah's witness on the night of Sabbath, I'm a magnet to divine attraction<br/>
Expressing rhythm with a primal passion<br/>
Dancing in the silent blackness, stepping in formation with the tribal patterns<br/>
Guided by this valley of the Nile magic<br/>
I follow shadows sundials cast in<br/>
I think I'm Michael Jackson<br/>
The one that MK Ultra spiked with acid to the night of homicidal passage<br/>
I'm not a DJ, but I was still breathing in the body bag<br/>
Clawing fingers vinyl scratching<br/>
To the sounds of Michael Jackson<br/>
I'll strike a match stick in the driest cabin, fire blasting I'm Spyro the tiny dragon<br/>
Burn this entire labyrinth and hide the ashes<br/>
I'll write Michael Jackson in bold, underline italics<br/>
Uppercase subtitled captions<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
L.S.D...<br/>
Cambatta<br/>
Grand Number TheoRam (GNT 1:1)<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
[Verse 3: Cambatta]<br/>
Mike El, Mikha'el<br/>
Which means Who is Like God when defined in Latin<br/>
Deeper than the cytoplasmics, quite elaborate<br/>
Watching movies in my mind make my eyelids spasm<br/>
If you could read my mind you'd hear a psycho laughing<br/>
Back yard got a lion and a tiger napping<br/>
Rollercoaster too, keep your seatbelts tightly fastened<br/>
Metaphor for the life I'm having<br/>
After a day of brain surgery<br/>
I enhance my third eye with glasses, I've discovered what your science hasn't<br/>
Divide a fraction to a final fragment<br/>
The universe is a uterus having wide contractions<br/>
I found a pen and the bible happened<br/>
I signed it Michael Jackson<br/>
Media stressing, need a spinal tapping they killed me and Prince<br/>
Whenever lightening happens it's the titans clashing<br/>
Crotch tightly grab it<br/>
Ladies passing out, got them falling like Mike Tyson jabbed them<br/>
Lisa Presley and Naomi Campbell tried to have him<br/>
But I denied their passes<br/>
Best womb is the test tube<br/>
Million other Michael Jacksons aborted inside of napkins<br/>
I cry every time it happens<br/>
They call me Michael Jackin'<br/>
My doctor was a trifling bastard<br/>
He's the reason why I'm relapsing<br/>
Forever I'm relaxing<br/>
I didn't get to say bye to Katherine...<br/>
Michael Jackson....<br/>
<br/>
<br/>
<br/>
From the darkness, Michael Blackson<br/>
<br/>
From the pipe, Michael Crackson<br/>
<br/>
From the music, Michael Jazzson<br/>
<br/>
I'm not my dad's son<br/>

### 13) L.S.D...

[Verse 1]<br/>
What is LSD, but a Little Strip of Destiny<br/>
When the Lonely Silence is Deafening<br/>
And my Living Situation is Depressing me<br/>
I'm repaying the Lord's Spiritual Debt to me<br/>
First time I took a Lethal Size Dose<br/>
But never will I Load Syringes with Dope<br/>
I remember being Lost Scared Delusional<br/>
Seen the same Lords the Soothsayer Druids do<br/>
Took a Ladder to the Seventh Dimension<br/>
The body is Literally Spirit Detention<br/>
Leviticus Scripture Describes<br/>
Moses Liberating Social Divides<br/>
Leading Sinners with the Diethylamide<br/>
Add a Little Salvia Divinorum, Leaves Stiff and Dry<br/>
From the forrest the Last Soldier to Die<br/>
Smoked bubba kush my Lieutenant Still Dan<br/>
<br/>
[Chorus]<br/>
What is LSD?<br/>
What is LSD?<br/>
What is LSD?<br/>
Lunar Solar Duality<br/>
<br/>
[Verse 2]<br/>
Lucifer Satan Devil<br/>
Logan Spawn Deadpool<br/>
The Lunatics Sadistic and Dreadful<br/>
Osiris Limbs Scattered and Disassembled<br/>
Time machine with the Lamborghini Style Doors<br/>
Extremely Limited Silverish Delorean<br/>
Why my head Look Slightly Deformative<br/>
Cuz my frontal Lobe Synaptics are Dwarfing them<br/>
And every time I Let Semen Drop<br/>
I create a Legacy of Super Demigods<br/>
I'm Luke Skywalker's Daddy, my red Light Saber's Darth<br/>
My Laboratory Secluded and Dark<br/>
Lyrics Sick as Dysentery<br/>
I'm a Living Speaking Dictionary<br/>
Mental Lexicon Sumerian Dialect<br/>
I see the image Like Spike Directs<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
Lunar Soular<br/>
Cambatta<br/>
Mic El JahXsun<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
[Chorus]<br/>
What is LSD?<br/>
What is LSD?<br/>
What is LSD?<br/>
Lunar Solar Duality<br/>
<br/>
[Verse 3]<br/>
LSD wears a Leopard Skin Dress<br/>
Her tongue kiss is tempting but her Lifted Skirt's Death<br/>
Her voice sexy a Latin Spanish Descent<br/>
Don't be the victim the Lady Serpent Detects<br/>
A lot of bumps on this Long Slow Drive<br/>
Should I give up and die no, Lord Shall Decide<br/>
Longevity Sufficiency and Diligence<br/>
Loyalty Stability and Discipline<br/>
Made it through a Lotta Soul Dissonance with Limericks Soliloquies of Dickinson<br/>
The king before Lebron Started Dribbling<br/>
Sometimes I ask myself what is love<br/>
It's Legitimately Serotonin Dopamine<br/>
The lack of it causes Looping Suicidal Dreams<br/>
Like you smoked LSD Laced Sour Deez<br/>
Mental Labyrinth Schizophrenic Dementia<br/>
My Lobotomized Skull is Dismembered<br/>
The tongue is but a Liquid Sword Dagger<br/>
Lyric Samurai Duel and Leverage Source Data<br/>
You would think I had a Law School Doctorate<br/>
You ain't never heard a Linguist So Dominant<br/>
Lip Spit Drooling, Lean Syrup Drowsiness<br/>
Lubricant Solvent Dissolve in it<br/>
LSD, Legendary Shaman Doctor<br/>
Control weather like a Linux Storm Doppler<br/>
I'm high pitch like the Late Star Doc Ellis<br/>
With the next Level Strike Diametrics<br/>
Refilling my Limitless Scripts Daily<br/>
Until my caskets Latent with Sweet Daisies<br/>
I Let Steaks Dangle, over head of Lost Starving Dogs<br/>
Supply fire Light Sun's Dawn<br/>
Never let a Liar Shuffle Decks<br/>
Black belt in Bruce Lee Self Defense<br/>
Show you the will to beast like what you see when you Leopard Stomach Dissect<br/>
Let the Stoners Digest<br/>
[Chorus]<br/>
What is LSD?<br/>
What is LSD?<br/>
What is LSD?<br/>
Lunar Solar Duality

### 14) Psylense of the Lambatta

Sunlight, moonlight<br/>
One night, mood right<br/>
New sight<br/>
Open my eyes and let the few write<br/>
New Christ<br/>
Birth<br/>
<br/>
Mary had a little lamb<br/>
Sherri had a little Cam<br/>
Carried him within her hand, married to a missing man<br/>
Buried under stricken land<br/>
Mary had a little lamb<br/>
Sherri had a little Cam<br/>
Miracle she didn't plan<br/>
Nothing makes saints like a sinner can, innerstand<br/>
<br/>
Grown man sleeping on the floor<br/>
Hear the mice squeaking by the door<br/>
I ain't really eating any more<br/>
Money spent on this bag of weed I can't afford<br/>
What's the meaning of it all?<br/>
Living in the Bronx where it's freezing in the fall<br/>
And police are on the call<br/>
Isolated from the people I adore<br/>
Family and friends I don't speak to anymore<br/>
Mama struggles she can't even get a call<br/>
Probably think that I don't need her anymore<br/>
I'm just working out my demons with the Lord<br/>
Put them deep into a song like I bleed when I record<br/>
I don't even like breathing when I'm poor<br/>
So I'm working til I'm rich enough, I can buy my freedom from the law<br/>
Or maybe I just need to be evolved<br/>
Maybe it's too deep for me to solve<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
Wings of Icarus<br/>
Cambatta<br/>
Lunar Soular<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
Mary had a little lamb<br/>
Sherri had a little Cam<br/>
Carried him within her hand, married to a missing man<br/>
Buried under stricken land<br/>
Mary had a little lamb<br/>
Sherri had a little Cam<br/>
Miracle she didn't plan<br/>
Nothing makes saints like a sinner can, living innerstand<br/>
<br/>
I get so preoccupied<br/>
I ain't know my uncle and my auntie died<br/>
Remember when I heard my grandmama died<br/>
Wasn't there to wipe the tears from mama's eyes<br/>
Little sister was, it had her traumatized<br/>
Should've been home on thanksgiving I apologize<br/>
The guilt that's in my spirit can't be quantified<br/>
And when I ain't have a father uncle John was mine, God I try<br/>
<br/>
Thank you, I thank you<br/>
You'll still be the one that I pray to<br/>
I still feel I have to be grateful<br/>
But why do you take back your angels?<br/>
I love you I hate you<br/>
But I didn't ask to be made you<br/>
Can't I relax and be stable?<br/>
Why does this have to be painful?<br/>
Mary had a little lamb<br/>
Sherri had a little Cam<br/>
Carried him within her hand, married to a missing man<br/>
Buried under stricken land<br/>
Mary had a little lamb<br/>
Sherri had a little Cam<br/>
Miracle she didn't plan<br/>
Nothing makes saints like a sinner can, living innerstand<br/>
<br/>
Already died I can't die no more<br/>
I'm alive and I wanna be alive some more<br/>
Already cried I can't cry no more<br/>
Feeling so high, why my eyes so low?<br/>
Try to shine and let my soul glow<br/>
It's a part of me inside even I don't know<br/>
Places in my mind even I won't go<br/>
This the encore to the final show

### 15) Wings of Icarus

Damn<br/>
<br/>
That nigga Cam man<br/>
Oh, wait, blow the smoke in the air<br/>
Pray, damn, Holy Ghost will appear<br/>
Oh man, Jehovah is here<br/>
Yeah partying, but nobody here<br/>
Damn, while I go up the stair<br/>
Floating, floating, while we float in the air<br/>
<br/>
<br/>
<br/>
Finally I'm flying, I just grew my wings**_<br/>
Look at them, they're beautiful<br/>
High up in the sky<br/>
So happy I can sing_**<br/>
Melody so beautiful<br/>
Finally I'm fly, I just grew my wings<br/>
Heaven is so beautiful<br/>
I just realized<br/>
I died and now I'm free<br/>
<br/>
<br/>
<br/>
I stick to the game plan<br/>
This is really my escape plan<br/>
They feed and lynch us from the same branch<br/>
And feed and whip us with the same hand<br/>
Damn, nothing motivate like pain can<br/>
Then the slave read, then the slave ran<br/>
I'm just trying to make it out this wasteland<br/>
Now a shepherd, was a stray lamb<br/>
Elevated this is Space Jam<br/>
He's king with the crown of an emperor<br/>
See upcoming rap shows<br/>
Get tickets for your favorite artists<br/>
You might also like<br/>
Psylense of the Lambatta<br/>
Cambatta<br/>
Camballah (Chokmah)<br/>
Cambatta<br/>
​euphoria<br/>
Kendrick Lamar<br/>
These genes that are found in molecular breeds wings that are found on the Khepera<br/>
<br/>
Bling bling, that's the sound of my neck-a-lace<br/>
Ching ching, that's the sound of my register<br/>
Ring ring that's the sound of my cellular phone<br/>
I might rise so high above the sky<br/>
That I might die if I don't spread my wings and fly<br/>
I might rise so high above the sky<br/>
That I might die if I don't spread my wings and<br/>
<br/>
Finally I'm flying, I just grew my wings<br/>
Look at them, they're beautiful<br/>
High up in the sky<br/>
So happy I can sing<br/>
Melody so beautiful<br/>
Finally I'm fly, I just grew my wings<br/>
Heaven is so beautiful<br/>
I just realized<br/>
I died and now I'm free<br/>
<br/>
Look in the sky what do you see?<br/>
<br/>
That's not a bird, that's not a plane, that was just me spreading my wings<br/>
Got off my knees, back on my feet<br/>
Now I feel free, like I can breathe, swift as the breeze<br/>
I'm on a cloud right now and I'm never coming down right now<br/>
I feel higher than a line right now<br/>
Getting ready for my crown right now<br/>
Moving at the speed of sound right now<br/>
I'm black and I'm proud right now<br/>
Queen ready for a gown right now<br/>
I'm so high right now<br/>
I can prove the law of gravity's a lie<br/>
I believe in my ability to fly<br/>
I don't even gotta smoke to get me high<br/>
As I float above you I look down and I say hi<br/>
Finally I'm flying, I just grew my wings\*\*\*<br/>
Look at them, they're beautiful<br/>
High up in the sky<br/>
So happy I can sing<br/>
Melody so beautiful<br/>
Finally I'm fly, I just grew my wings<br/>
Heaven is so beautiful<br/>
I just realized<br/>
I died and now I'm free

## Camballah, Volume 1 (27 APR 2018)

### 1) Crown of Thorns (Kether) Lyrics

(Yeah.. God)<br/>
What do you expect from a lord like me?<br/>
(Batta..)<br/>
(Lord.. God)<br/>
I proclaim in harmonious accord<br/>
Holy is the Lord, holy is the Lord<br/>
Roll me in the morgue, throw me in the floor<br/>
Put me in a dark cave, roll a boulder over door<br/>
Holy is the Lord, holy is the Lord<br/>
More pain than a soldier can endure<br/>
Holder of the sword, Conan in the war<br/>
Chosen one is born, roses full of thorns<br/>
Holy is the Lord<br/>
Dark lullaby of the smart, colored guy<br/>
Large cluttered mind, but a sharp hunter's eye<br/>
Cry blood in the water, it's shark supper time<br/>
Jumped and dived in like a cannon ball and twenty died<br/>
Eat the meat, collect the teeth and pluck the eyes<br/>
Walls have skulls of rare species, a hundred kinds<br/>
Mummy shrine, like the one that Danny Glover finds<br/>
In Predator<br/>
, and some are mine from my double lives<br/>
Jump in time like Flubber slime, hunt the other I's<br/>
Kill twelve and stand lone like the sun and shine<br/>
Numb inside - ever since my grandmother died<br/>
I never knew so many tears can come from an eye<br/>
Wonder why, the money sign is a caduceus?<br/>
Reveal the snakes in the staff that you moving with<br/>
Studious Nubian,<br/>
sufi who Tahuti is<br/>
Reducing truth to the nucleus, you get used to this<br/>
Callous now, bat catching but I don’t use a mit<br/>
Read palms, Caught the ball before he threw the pitch<br/>
My super suit equips unusual accoutrements<br/>
The hooligan of the Rosicrucian tutelage

### 2) Camballah (Chokmah) Lyrics

[Verse 1]<br/>
Am I Cambatta or Camballah?<br/>
My tree of knowledge is the<br/>
plant changa<br/>
Innerstand Allah<br/>
Body matter is shifting amorphously as glowing lamp lava in weed man casa<br/>
I demand dollars, diagram is a<br/>
mandala<br/>
Gram died, now she Samsara<br/>
With the<br/>
Grand Dharma<br/>
Spread seeds playing<br/>
Mancala<br/>
, cultivate you, I'm a man farmer<br/>
Desert sand gardener, stone hand carver<br/>
Trim crops, I'm a land barber<br/>
Cam, Candyland, Wonka, the glucose for ant larva<br/>
Weapon advanced, clamped, I am<br/>
D.A.R.P.A<br/>
Deep as Agartha<br/>
, Chief for the Shambhala<br/>
Earth flat, I'm off edge, I ran farther<br/>
Polyglot of gematria<br/>
When I'm talking to Jah I got a stenographer<br/>
I pray to myself I'm not an idolater<br/>
Allah Sallallahu 'alaihi wa sallam<br/>
Before I was able to hold the bottle up<br/>
Mama gave me a marker, I drew the Kabbalah<br/>
Cobbler, give me a foot I take a kilometer<br/>
Thirsty, I drink the mercury from a thermometer<br/>
Get your product up<br/>
I could breathe in an empty jar and then sell it for a profit at the market bruh<br/>
Francis Coppola's Dracula, godfathered em'<br/>
Monsterous,<br/>
siphon the body's blood of Phlebotomists<br/>
Batta got his colostrum up, I give her obelus<br/>
Her twat'll bust open like the mouth of a hippopotamus<br/>
That's a portmanteau for hip hop anonymous<br/>
Like turducken and liger, and tigon and such<br/>
Flowdysseus, odyssey, Batta ominous<br/>
Rock a Oculus as binoculars, watching Omnitrix<br/>

### 3) Harim Abiff (Binah) Lyrics

Harim Abiff, Theorem legit<br/>
Son of a widow, Tyrion Prince<br/>
Appear in a glyph, Sumerians writ<br/>
Before awareness of Aquarian shift<br/>
The hammer of Kane, I carry in fists<br/>
I build a temple with ethereal bricks<br/>
I steer imperial ships<br/>
Chariot with arial lift<br/>
Gravity, I clearly resist<br/>
Dogon with the<br/>
seriousness<br/>
A ruffian would murder for the chair that I sit<br/>
My black diet make an Aryan sick<br/>
Piss - on the torch Luciferians lit<br/>
Rich -<br/>
checks<br/>
Like a cereal mix<br/>
Kiss - death<br/>
You still in fear of the bitch<br/>
Derringer spit like Barrington's lips<br/>
Levy, they broke it<br/>
That is not conspiracy myth<br/>
Trip<br/>
Flood earth to a river like Styx<br/>
By the heel I was carefully dipped<br/>
I cannot die (Why?)<br/>
I cannot die (Why?)<br/>
I cannot die (Why?)<br/>
I cannot die (Why?)<br/>
I flood earth when I cry<br/>
Looking in the sky's really looking in my eyes<br/>
I cannot die (Why?)<br/>
I cannot die (Why?)<br/>
I cannot die (Why?)<br/>
I cannot die (Why?)<br/>
Greatest architect of my time<br/>
And I'm my most masterful design<br/>

### 4) Golden Child (Chesed) Lyrics

Story of the boy that never breathes<br/>
He never bleeds, royal oil he secretes<br/>
Born with all the joy he'll ever need<br/>
He's all knowing, no one taught him how to read<br/>
Baptized in the Sinai Peninsula<br/>
Described WiFi to Nikola<br/>
Mutant academy, sci-fi curriculum<br/>
Journey earth, find tribes, trip with em<br/>
Universe is a touch screen<br/>
Rearrange sky when he wave bye<br/>
Double click sun it'll switch night<br/>
Make a cloud rain with a swift swipe<br/>
If you try it then it won't work<br/>
It only activates when God fingerprints type<br/>
End is near, sit tight<br/>
Watch stars like an episode of it's life<br/>
Elaborate and eloquent<br/>
His memory is him imagining remembering<br/>
Lost looping through the labyrinth as regimen<br/>
And most humanoids are actually content with it<br/>
Feet traveling on relatives, delicate<br/>
Granddaddy skeleton is graveling the sediment<br/>
His true shadow is dimensionless<br/>
Sisyphus, rolling a boulder back up an endless cliff<br/>
Dollar reads annuit coeptis<br/>
Branded with American deception<br/>
You a sheep<br/>
That's (f)lannel in your sweat drip<br/>
Inherited a death wish of parents that were less fit<br/>
This is Cameron's redemption<br/>
Peculiar child Miss Peregrine protected<br/>
Reflective in the shadow of the one God<br/>
Hand puppet, then its kettle in projection<br/>
Dark skin has botanical connections<br/>
Higher self has an amethyst complexion<br/>
He's the one answering the questions<br/>
He holds spirit in his animal appendage<br/>
You are but a sample of the vestige<br/>
Black panther is a cancer to Jesuits<br/>
Disasters bring planet's new aesthetics<br/>
I just hope I see my grandma standing at the entrance<br/>
Profound in ability<br/>
He speaks in the sound of calligraphy<br/>
The hidden links found in his imagery<br/>
Lost in the sea, drowned in fertility<br/>
<br/>

### 5) Theory of Everything (Geburah) Lyrics

[Verse 1]<br/>
A trillion shades in my color spectrum<br/>
I exist within a sub-dimension<br/>
I'm impossible's one exception<br/>
Plasma from the sun and the bloods connected<br/>
Time's a serpent with the tongue extended<br/>
Mouth swallowing the tail, so begun the ending<br/>
Most religions are just sun obsession<br/>
Virgin Mary is just cunt obsession<br/>
I paint sound and I speak paint<br/>
That's two types of just one expression<br/>
This technology ain't done progressing<br/>
Until God in us become reflections<br/>
When I'm alone I feel another presence<br/>
Heaven's up, but in space there's no up direction<br/>
I kept a bottle of placenta from my birth<br/>
I get sick and sip the juices from my mother's essence<br/>
[Bridge]<br/>
I watched the clouds as they meta-morph<br/>
Walk around aimlessly like a headless corpse<br/>
From a place where the unloyal don't get remorse<br/>
Unless its about money, you don't get to talk<br/>
[Verse 2]<br/>
The universe is rendered as I see it<br/>
So people don't exist until I meet them<br/>
Tree falls I don't hear it, it ain't happen<br/>
I crack Fermat's Theorem on a napkin<br/>
Prometheus made the fire just to heat the piff<br/>
Any human with a badge is a piece of shit<br/>
Women's mouths water when they see the dick<br/>
Cause if they swallow they'll inherit all this genius-ness<br/>
Gods writing down names and I've seen the list<br/>
It says me and me and me and me and me and him<br/>
Or her, now - gender is blur<br/>
There is no thing that never will occur<br/>
Time is a cool way to remember where we were<br/>
I'm dropping breadcrumbs<br/>
I'm with Gretel on the search<br/>
Space is a neighborhood<br/>
The ghetto is the earth<br/>
Before it gets better it gets worse<br/>

### 6) Babylonian Mordecai (Tiphereth) Lyrics

All hail, is it well with thee?<br/>
Before I speak I get permission from the elderly<br/>
Patiently waiting for the bell to ring<br/>
I'm fighting temptation that put a spell on me<br/>
Bloody colon, knuckles swollen<br/>
Buster Douglas in his lucky moment<br/>
Stolen belt, buckle Golden<br/>
Clutch Vulcan, Sultan<br/>
Son of Odin, chosen<br/>
Drunk a potion from a bubbling cauldron<br/>
Coping<br/>
My capacity for love is frozen<br/>
Left my inner-Romeo like young DeRozen<br/>
Dumped my soul twin, brung the hoes in<br/>
Rumps bulging - Double throated - Scoliosis<br/>
Arch your back til your butt and nose hit<br/>
Under drug hypnosis<br/>
And my mother knows it<br/>
Guns, roses<br/>
Buzzing locust<br/>
Another omen that begun unfolding<br/>
Giants get to Muggsy Bogues-in'<br/>
Son fly with the wax wings of Icarus<br/>
Return of the Black King is imminent<br/>
Vital organs are actually instruments<br/>
Feeling lit, pass me the filament<br/>
Live a myth, mad deep predicaments<br/>
Finna rip, athletes with ligaments<br/>
Pack need a split in it<br/>
Little infant speak native tongue fluidly<br/>
And pass it as gibberish<br/>
I phonetically spell teen with I in it<br/>
Let me borrow your bike, I be back in five minutes<br/>
You won't see me for a week or two<br/>
And when you do, I won't even remember meeting you<br/>
You know that little voice you hear deep in you?<br/>
Mine only says "I'm God" in repeating loops<br/>
Ghost illustrator<br/>
It's me, it's true<br/>
Sneaking through everything Alex Gray think he drew<br/>
I've seen a blind baby play peekaboo<br/>
Even seen a few Pikachu's out in East Peru<br/>
Reality's a fallacy you think is true<br/>
If you don't believe in me, I don't believe in you<br/>
Unidentifiable to normal eyes<br/>
As I stare at the horizon, I see Horus rise<br/>
Getting comfortable with death<br/>
Before I die<br/>
Mortal man on the surface, Immortal Lord inside<br/>
Higher than the pitch when the porpoise cries<br/>
Talking to the dolphins<br/>
This is John Lily's story time<br/>
As I journey this imaginary portal ride<br/>
Prophecy of the Babylonian Mordecai<br/>

### 7) GroundGods Day (Netzach) Lyrics

I wake up and do this shit everyday<br/>
Everyday<br/>
Everyday<br/>
I do this everyday<br/>
I wake up and do this shit everyday<br/>
Everyday<br/>
Everyday<br/>
I do this everyday<br/>
I used to never pray<br/>
Until I found out that [?] jake jumped and murdered my dad<br/>
Now he rest in a better place<br/>
I'm trying to get away from these ghetto ways<br/>
I refuse to be led astray<br/>
Death is the best escape<br/>
I let heaven wait<br/>
It don't matter the stress I take<br/>
Mama the energy<br/>
But somebody gotta pay the rent today<br/>
Gotta be the man and wipe the debt away<br/>
But the more you work its like the less you make<br/>
Got me out here wildin' trying to sell an eighth<br/>
'Til I elevate<br/>
I could sell estate<br/>
That's a better way<br/>
Leave a legacy<br/>
Man, I feel like it's been so hard for me to meditate<br/>
(...Ou)<br/>
Excuse me while I give my head a break<br/>
Work is never done, it's always to early to celebrate<br/>
Started so far below the bottom, Batta was never Drake<br/>
Victory sweet as a carrot cake, I need to get a taste<br/>

### 8) Blxssed Up (Hod) Lyrics

Blessed up<br/>
I'm blessed up<br/>
I'm blessed up<br/>
Next up<br/>
I'm next Tut<br/>
Blessed up<br/>
I'm blessed up<br/>
I'm blessed up<br/>
Next up<br/>
I'm next Tut<br/>
Guess what?<br/>
There will never be a next us<br/>
Burn the center of the nexus<br/>
Where the hammers bang<br/>
Like a doctor do in a checkup<br/>
Tech's bust, you a dead duck<br/>
Til' the checks come<br/>
Like a hedge fund<br/>
Water whipping I'm the juice man<br/>
O.J. with the left glove<br/>
White girl, I'ma cut her up<br/>
Do the Dexter<br/>
I'ma cut her up like the bread crust in my breakfast<br/>
Selling point one for the ten bucks<br/>
White people are the best fiends<br/>
And white people are the best plugs<br/>
Kokaina give me head rush<br/>
Sassafras got me sped up<br/>
Dabbing with the hand that fed us<br/>
Trigger finger got the bed bugs<br/>
I get up like a hogfly, I'm the web spud<br/>
Put a rack on it when the rapper spit<br/>
Leave the web spun<br/>
When I crack the whole Xanax in half<br/>
I'ma call that shit a special ed bus<br/>
Roll the next blunt

### 9) Tears of Yakub (Yesod) Lyrics

Have you ever seen a goat and a lamb?<br/>
A slug and a pig?<br/>
A bird and a beetle?<br/>
I'll make you duck from the Eagle<br/>
And put a pigeon pussy on a cock<br/>
And breed you<br/>
The island of Dr Moreau<br/>
The science I drop is occult<br/>
Doctor Moreau - More O<br/>
I'm a more with O's<br/>
The more I rose I rise, adopting my role<br/>
I create man like the God's do<br/>
Yakub, dilute black dot to white you<br/>
Red pill<br/>
Blue pill<br/>
Cryptic<br/>
Piru<br/>
Three point<br/>
One four<br/>
Infinite<br/>
Cycle<br/>
It's six<br/>
Six six<br/>
Times two<br/>
Triple it<br/>
I view<br/>
Mystic<br/>
Rituals<br/>
I use<br/>
Genetic alchemy<br/>
Supreme mathematics<br/>
With this dick, one plus one can amount to three<br/>
Comedic seraphims are surrounding me<br/>
The invention of the mirror keeps astounding me<br/>
The mirror’s like a live-action camera<br/>
Cam-e-ra, Cam’s era<br/>
I so high like shooting in the sun but I glance clearer<br/>
If you blind then you can’t hear em<br/>
If the size of my brain reflected my knowledge<br/>
My forehead would be the size of Rihanna’s<br/>
I’m being honest<br/>
Tetragrammaton, I’m Imhotep with a sceptre<br/>
The architect that can lift a brick with a Cameron song<br/>
He’s an alien, Ai-leen, L I ON, I smoke L’s for eons<br/>
See, How I break it down?<br/>
Manipulate your language and create a sound<br/>
Only audible to the descendants of the ancient crown<br/>
Would you sacrifice your sky just to save the ground?<br/>
Would you sacrifice your future just to save the now?<br/>
Would you sacrifice your gold just to save your brown?<br/>
I’m half African and half Native<br/>
Two of the most oppressed groups ever<br/>
Them past Aryans was, mad racist<br/>
Backlashes to the black nation<br/>
Bad pathogens and castrations<br/>
I’m half [?] and half tainted<br/>
I’m half arrogant and half gracious<br/>
This track captures what that’s saying

### 10) No Fear (Malkuth) Lyrics

No fear, no fear<br/>
No fear, no fear<br/>
No fear, no fear<br/>
No fear, no fear<br/>
No fear, no fear<br/>
No fear, no fear<br/>
No fear, no fear<br/>
No fear, no fear<br/>
All black from the soles up<br/>
Levitating on an old rug<br/>
Nail my body to a gold crux<br/>
Lord God but I don’t judge<br/>
Smoke bud but I won’t budge<br/>
Doe flood like a broke tub<br/>
Sold drugs, coke nose<br/>
Lunch, dope, dust<br/>
Trippin’ like a coach bus<br/>
Mush mouth<br/>
Smuggle dope in Mama kangaroo’s puss pouch<br/>
Hood grouch<br/>
Exhale, kush clouds ‘til a nigga look Laos<br/>
Grillin' me will get you cooked out<br/>
Recipe will make a cook shout<br/>
Money growing like a wood snout<br/>
Real boy from a juug house<br/>
Every stoner need a good couch<br/>
Took Crown<br/>
Don King with the book bout<br/>
Au-thor, lift a heavy hammer you get put down<br/>
Bloody Mary<br/>
Bloody Mary<br/>
Bloody Mary<br/>
Staring in the old mirror, suddenly, a weird, scary hoe appear<br/>
I ain’t care - hit her in the derriere, right there

### 11) Ego Death (Daath) Lyrics

I'm left alone<br/>
I feel like someone's watching me<br/>
And then I die<br/>
And when I opened up my eyes<br/>
I saw a suited man with a mic as he walks to me<br/>
Curtains drawn<br/>
Audience applauding me<br/>
Chanting as a gorgeous broad's awarding me<br/>
Rose from my seat, awkwardly<br/>
Touch my head and felt the headset and cords on me<br/>
Clearly, they're recording me<br/>
Big screen showing my point of view accordingly<br/>
And visions I don't want to see<br/>
I turned and noticed that the chair that I was sitting in<br/>
Is fitted with some virtual reality equipment shit<br/>
Then it dawned on me<br/>
The world that I was living in<br/>
Is just a simulation that I only spent a minute in<br/>
I was so shocked<br/>
I had a heart attack and died from the adrenaline<br/>
Then woke up in my bed again<br/>
With blurred visioning<br/>
I seen the silhouette of oddly shape headed men<br/>
With little skinny skeletons<br/>
As soon as I could see them I was dead again<br/>
Now I can't remember them<br/>
Now I can't remember me<br/>
Naked on the cold floor trembling<br/>
Struggle to my feet<br/>
Stumble to the sink<br/>
Cloudy water wet my skin<br/>
Open eyes, see the mirror<br/>
But I don't know who that man in reflection is<br/>
Yet he lives, who the hell is this?<br/>
Where's my pants? where's the kicks?<br/>
Couldn't find em' so I exited extra quick<br/>
Stepped out where the desert is<br/>
Out where Kemet is<br/>
All I see is sunset foreverness<br/>
Travel forty days to the precipice<br/>
Then I slipped<br/>
Jumped off the edge of it<br/>
Saw the light at the end of it then went to it<br/>
As it opened I saw medics and my relatives<br/>
Mama too, I guess heaven's relative<br/>
Life is so repetitive, it never quits<br/>
'Til you experience what all of your potential is<br/>
The fear of death is slaving you<br/>
It's changing you<br/>
It's making you afraid to do<br/>
The things that you were made to do<br/>
We in a place where your creator animated you<br/>
For training you<br/>
And testing all the strength in you to make it through<br/>
You never fade<br/>
You just replay in complicated loops<br/>
Until you reach your fate<br/>
And then the gate in heaven waits for you<br/>
If heaven's fake<br/>
Then next dimension as a state is cool<br/>
I thank my maker, then he thanked me cause I made him too<br/>
In my worst times, I practiced death<br/>
So proficient, I could do it in my first try<br/>
Pass the test, unwrap my flesh<br/>
Past the acid tab attempts and orgasmic sex<br/>
Caps and stems, bags of wet<br/>
DMT ain't doing justice to an actual death<br/>
Moments after your last gasp for breath<br/>
Feels better than when you had the breath<br/>
The astral quest is [?]<br/>
Allow me to lead you through the dark<br/>
Feel free to board the ark<br/>
Built with a design based on prehistoric sharks<br/>
Sail through sound waves that are beating in your heart<br/>
As I breathe it seems the frequency is sharp<br/>
Then it flat lines<br/>
My body is deceased and I depart<br/>
I've seen the geometrics you graffiti in your art<br/>
It's your ancestors speaking through the genius that you spark<br/>
They've foreseen it with the charts<br/>
The last afterlife mapmaker<br/>
The cartographer, the path tracer<br/>
Purgatory's first black mayor<br/>
Mountain peak flag placer<br/>
Die while I'm dead, I'll back be up in that manger<br/>
Highly adaptable mass changer<br/>
Shapeshifter<br/>
Water when it's gas vapor<br/>
I dissipate and reformulate it<br/>
Cause that's nature<br/>
Spread a seed as I'm trail blazing<br/>
A grass grazer<br/>
Praise the Revenant<br/>
Grizzly bear wrestling<br/>
Die and come back<br/>
Vision clear ever since<br/>
Think about it as I'm in my chair trembling<br/>
Sitting here, penciling<br/>
Scripts for weird medicines<br/>
Really rare specimens<br/>
Sipping sheer mescaline<br/>
Returning spirit on a sixty year regimen<br/>
I'm the living dead that isn't dead<br/>
With a missing head that's still ahead<br/>
You think you're awake but you're still in bed<br/>
Die for the fun of it with Bill and Ted<br/>
Fridge full of goat blood and chicken legs<br/>
Life is just hatching in a little egg<br/>
That's actually in a bigger egg<br/>
Crack it then the hole will be too big to mend<br/>
Greatest starts have the quickest ends<br/>
Once you see the patterns you'll predict the trends<br/>
As I'm glimpsing in my inner-lens<br/>
If you don't than you're like Sampson when they clipped his dreads<br/>
Just follow what the scripture says<br/>
My dreams are so real, I saw a toilet and I pissed the bed<br/>

### 12) Dark Light (Thaumiel) Lyrics

This little light of mine<br/>
I'm bout to let it shine<br/>
This little light of mine<br/>
I'm bout to let it shine<br/>
All of us men are fly<br/>
How come we never ride?<br/>
Blessed with a set of eyes<br/>
That's how I led the blind<br/>
This little light of mine<br/>
I'm bout to let it shine<br/>
This little light of mine<br/>
I'm bout to let it shine<br/>
I'm so ahead of time<br/>
If you feel like you doubt me then get in line<br/>
Now I know that a God could be never poor<br/>
And that's the reason I know that I'll never die<br/>
Let me shine<br/>
Sleep is a thing of the past now<br/>
Golden calf, I'm the cash cow<br/>
Yellow sun with the black crown<br/>
Gunshot shattered glass house<br/>
All I'm hearing in the background<br/>
I'ma give you to the count of ten<br/>
To get your kiester off of my property<br/>
One.. Two.. TEN!<br/>
Police gonna have to call the cops on me<br/>
I get high and I play three on three<br/>
Teams will be<br/>
Me on me on me on me on me on me<br/>
Chief a ganja leaf, see beyond belief<br/>
Little Brenda had a baby<br/>
And I heard her baby just had a baby too<br/>
If I claimed all the babies on my taxes<br/>
I could probably start a baby zoo<br/>
Raise em up like a NAVY troop<br/>
Have em shooting Uzis by the age of two<br/>
Aim at you<br/>
Blung Blung Blung Blung Blung Blug<br/>
Look what you made me do

## Holy Ghost 2 (13 September 2019)

### 1) The Conjuring (Intro) Lyrics

Introduction of soundbites from different interviews with Camabatta on the BlackMagik363 YouTube Channel<br/>
Chorus:<br/>
(Eye)<br/>
Go so deep<br/>
Go so deep<br/>
Go so deep<br/>
(Eye)<br/>
Go so deep<br/>
Go so deep<br/>
Go so deep<br/>
(Die)<br/>
Don’t know me<br/>
No mo<br/>
Ego So free<br/>
(Blind)<br/>
Don’t know evil<br/>
No evil know me<br/>
(Eye)<br/>
Go so deep<br/>
Go so deep<br/>
Go so deep<br/>
(Eye)<br/>
Go so deep<br/>
Go so deepd<br/>
Go so deep<br/>
(Time)<br/>
No roley<br/>
Don’t go sleep<br/>
Don’t know sheep<br/>
(blind)<br/>
Don’t know evil<br/>
No evil know me

### 2) Journey of Heru Lyrics

[Intro: Rafijah Siano]<br/>
Stood from afar, look on his face he was a child<br/>
Who came to rage war, to we the victors belongs the spoils<br/>
[Verse 1: Cambatta]<br/>
Go O.D., So goatie<br/>
Grow goatee rose gold teeth, Polo tee<br/>
Gaudy, godly, sewn clothing<br/>
Goku's foe Broly no homies, old Roshi<br/>
Jujitsu, roll no gi<br/>
Told coach please, don’t coach me, hold trophy<br/>
Spoke hope speech, glow holy, No rosary<br/>
Off axel, So Foley<br/>
New Kwame, old Stokely, so cokely<br/>
So Kunta no Toby<br/>
You don’t own me, you don’t know me<br/>
I’m grown Mowgli, left me in a hole lonely<br/>
Cold boney, hungry, I seen Satan I know Crowley<br/>
Abduct me then go clone me<br/>
Robo cop vs. robo me<br/>
44 squeeze, popo bleed, Flo-Jo speed<br/>
Face Olmec, pre date old texts<br/>
Created the tech that I gave Toltecs<br/>
Came to the west on my own soul trek<br/>
Hotep, mutant my belt buckle a gold x

### 3) Shaka Zulu Lyrics

[Verse 1: Cambatta]<br/>
Young brother from the gutter<br/>
Always been a fighter never been a runner<br/>
Mama was a hunter, daddy was a hunter<br/>
All my brothers hunt each other<br/>
Known to knuckle up and upper cut a slugger<br/>
Slug and punch and snuff and stun a thugger<br/>
Gonna stutter stutter blood a sputter<br/>
You gon do the Brooklyn bruk up<br/>
Buck em gun a drummer<br/>
Father thought I was a parasite in momma belly but he had it wrong<br/>
He ain’t know he had a spawn of a warlord 'til in 9 months I was born<br/>
Big black strong body of Lebron, I’ma be a king killing all pawn<br/>
Better be in form when I blow the horn bringing in the dusk Waking up the dawn<br/>
Looking at a God, prophesied by the shaman voodoo<br/>
Seen it all through the eye of Horus that I watch and view through<br/>
There was other warriors before me but they not this brutal<br/>
All this money but I’m not Mobutu<br/>
You down know me of forgot now you do<br/>
[Chorus: Cambatta]<br/>
Shaka Zulu<br/>
Shaka Zulu<br/>
Shaka Zulu<br/>
Shaka Zulu<br/>
The call me Shaka Zulu<br/>
I’m at the top of Khufu<br/>
I got the power who knew<br/>
Why would a god salute you<br/>
They call me<br/>
Shaka Zulu<br/>
Shaka Zulu<br/>
Shaka Zulu<br/>
Shaka Zulu<br/>
My name is Shaka Zulu<br/>
I’m at the top of Khufu<br/>
I got the power who knew<br/>
Why would a god salute you

### 4) Boss Talk Lyrics

[Verse 1: Cambatta]<br/>
Think I got the Holy Ghost, I don’t even got a pulse<br/>
I don’t got a lung left still I tell them that I’m ready for the smoke<br/>
Turn a L into a roach, I’m whipping the Ice cream Coke float<br/>
My team full of goats, If I ain’t the Christ king then I’m close<br/>
My genes in her throat, I sell her a pipe dream when she woke<br/>
I could've been 19 selling dope now I got them like fiends selling quotes<br/>
Pen is spelling what you won’t, Inner seven headed devil get evoked<br/>
My temple a 5 elemental host, my mother was still pregnant when I spoke<br/>
I️ was born without a belly button, starving cuz I don’t connect to nothing<br/>
Willy Wonka let me ride up in his glass elevator then I press the button<br/>
Thanking God that he invented cumming, it's a bird box never let the son in<br/>
Careful who I let genetics up in unless she got a womb in her neck or something<br/>
[Chorus: Cambatta]<br/>
I do the boss talk, all I’m talking is the boss talk<br/>
All you talk about is small talk, don’t be talking when the boss talk<br/>
I paid the boss cost, all I'm talking is the boss talk<br/>
All I'm talking is the cloth talk, got the knowledge that the gods taught<br/>
I do the boss talk, you be talking like a dog bark<br/>
No bite, quiet when the boss talk, when I floss I’ma talk sauce talk<br/>
I wear the boss cloth, yall soft when the boss talk<br/>
You ain’t even in the ball park, Got them calling me the boss boss<br/>
[Verse 2: Cambatta]<br/>
I come from under the underground, I feel ltike Harriet Tubman now<br/>
Father time like a dead beat dad to me cuz he always running out<br/>
We all Mother Earth's kids but she cold to us 'til her sun come around<br/>
Tummy growl when I hunt and prowl, 6’3" weigh a couple hundred pounds<br/>
Wearing earplugs and a blindfold I can still smell how a color sounds<br/>
Bloody hound I can find where the money found while I’m in a another town<br/>
I would have get a couple lobotomys If I ever had to dumb it down<br/>
Do the bucket list then I shit in the bucket and turn the crabs in the bucket brown<br/>
I get higher than Orion belt, If Orion was a ghetto black man like me<br/>
You wouldn’t find the belt unless it’s a Gucci designer belt<br/>
I dont moon walk but I sun run til the bottom of my Nike melt<br/>
Smoke toad with a Mayan elf, had a meeting with my higher self<br/>
I get higher than a chipmunk voice, how you woke you ain’t trip once<br/>
Seen my uncle cook a brick as a kid young white girl nip tucked<br/>
Pistol with extended clip make my pants bulge out like dick does<br/>
Pussy was made to addict us fucking 'til I bust dick dust<br/>
Let a clip bust put a hollow in a tip cup<br/>
Buck buck buck everywhere like I'm throwing dollars at the strip club for the big butt<br/>
So aware I'm a wolf, mouth running hoarse throat got a hoof<br/>
Burn bush climb mount Sinai came down with a book, look

### 5) Last Breath Lyrics

[Verse 1: Cambatta]<br/>
Feet hurting<br/>
World full of busy bees working<br/>
I ain't never met a free person<br/>
I don’t get along with these earthlings<br/>
I’m trying to seek purpose<br/>
Fight for something I believe’s worth it<br/>
Feel the curse I’ma reverse it<br/>
I don’t dream cuz I sleep nervous<br/>
Yet I Keep flirting<br/>
Face death like a Steve Irwin<br/>
Hold heat I’m a drink thermos<br/>
Tell the bartender keep serving<br/>
I’m trying to be perfect<br/>
Using dirty shit to clean dirt with<br/>
Only happy when the weed burning<br/>
Traded oxygen to breath herb in<br/>
Til I see curtains<br/>
Lungs failed and they cease working<br/>
Air is something that I need urgent<br/>
Suffocating trying to squeeze words in<br/>
[Bridge: Cambatta]<br/>
What would I do with my last breath<br/>
Would I yell, would I cry, would I laugh<br/>
Cuz I’m glad that I’m passed that mess<br/>
Til I pass never felt that bless<br/>
Even bad breath when you living<br/>
Is better than good breath when you lack flesh<br/>
Got a glass chest that I cracked<br/>
And my lost breath hasn’t made it back yet

### 6) SpellBound Lyrics

[Verse 1: Cambatta]<br/>
I don’t want a situation<br/>
Told her that I wanna keep it basic<br/>
I know this is gonna sound abrasive<br/>
All I really want is recreation<br/>
I ain’t ready for relation<br/>
Not the kinda nigga you can date with<br/>
Only make a reservation when I'm at a Days Inn<br/>
Bring another condom cuz I know I’m gonna break it<br/>
I don’t wanna end up like another Usher Raymond<br/>
It was so much harder to deny you when you naked<br/>
It’s rare that I would even stay to have a conversation<br/>
You somebody to relate with, a lady I can lay with<br/>
On more than one occasion<br/>
[Chorus: Cambatta & Songbird]<br/>
I think she put a spell on me<br/>
Hit me with the kinda loving you can still smell on me<br/>
I think she put a spell on me<br/>
I never knew there really was a heaven 'til it fell on me<br/>
[Verse 2: Cambatta]<br/>
Beauty is her name<br/>
I seen her dancing in illuminating rain<br/>
I knew it in my heart before I knew it in my brain<br/>
With you it’s like the present and the future are the same<br/>
You're alluring and appealing<br/>
Adorable, your energy is warming and it's healing<br/>
Assuring and revealing my aura in the ceiling<br/>
But my body on the floor because I’m kneeling, it's more than just a feeling<br/>
If a goddess what a god is<br/>
Then everything we got is what she got us<br/>
You be Aphrodite I’m Adonis, ironic as Alanis<br/>
I think you oughta know what's in my pocket<br/>
I just wanna make you smile for a while<br/>
Take you outta town, put a towel down, lay around<br/>
How it sound? Get your hair style for a crown<br/>
Your virginity was lost now it’s found

### 7) BlxkNxggx Lyrics

[Chorus: Cambatta]<br/>
I'm a Black nigga, half saint half sinner<br/>
I’m a Yak sipper, love Henny but it's giving me a bad liver<br/>
Dab hitter, not an addict I'm a bad quitter<br/>
Mac pimper pick a chick up in an Ac Vigor<br/>
You a bad stripper but you’ll never fit this glass slipper<br/>
Booty mad bigger ass thicker than your last picture<br/>
Gotta smash wit her back splitter make her splash river<br/>
I'm a cat killer, drown pussy it's a bad swimmer<br/>
[Verse 1: Cambatta]<br/>
I might roll a blunt up on the subway<br/>
I might be the pluggy that your plug pay<br/>
All this sauce money I'm a young Jay<br/>
I just hope my baby mama a Beyonce<br/>
Skinny waist booty looking plus shape<br/>
Bet I hit it raw after one date<br/>
I just crush a lot, that's what Pun say<br/>
All this sinning still I wake up praying every Sunday<br/>
Hoping that her period don't come late<br/>
I'll be paranoid for a month straight<br/>
Plus i got a trial for this drug case<br/>
Hand on the Bible I be lying in the judge face<br/>
Just product of this rough place<br/>
Bullet holes in my kitchen wall for the Feng Shui<br/>
Bullet goes in and outta men like they guns gay<br/>
Mama we gon make it out this hood someday

### 8) Pardon Me Lyrics

[Chorus: Cambatta]<br/>
Pardon me all of my people are part of me<br/>
See the police and they plot on me they don’t believe in equality<br/>
Pardon me, all of this heart is a part on me<br/>
They wanna Khalid Muhhamed me all of my army in harmony<br/>
Pardon me, I got alot of the pot on me<br/>
They got a copper to follow me, I got Obama to pardon me<br/>
Pardon me, I gotta start an economy<br/>
Call me the god of monopoly, they wanna Malcolm and Martin me<br/>
[Verse 1: Cambatta}<br/>
Shoot at me<br/>
They ain’t know a nigga bulletproof there ain’t shit you can do to me<br/>
Couldn’t kill a cam even with a diplomatic immunity<br/>
Anything you shoot at me I shoot at you we do it in unity<br/>
Soon as I tickle a trigger i bust it, it’s going through puberty<br/>
Bullet Hollow with a tip on it leaving you a gratuity<br/>
I might even shoot the funeral up while they reading your eulogy<br/>
Put a crystal in a pistol, it hit you, you wear it as jewelry<br/>
I don't fuck with the coonery<br/>
I'm a mutherfucking lab rat, you the brother from the rat pack<br/>
Got a gun up in the backpack, brap brap, cat nap<br/>
Bust a knuckle from the back slap skull is coming out his dad hat<br/>
Hope a piggy got Aflac, Shucky ducky ducky quack quack<br/>

### 9) Yahawashi Lyrics

[Verse 1: Cambatta]<br/>
I thought I told you I was high<br/>
I'm Yahawashi, y'all wish y'all was I<br/>
Waving Allah hi, but Allah was shy<br/>
Wanna wash ya eyes, Ayahuasca wise<br/>
Pot of agua for the caapi vine<br/>
You gotta die to get the knowledge that duat provides<br/>
I botanize sycotropics that are not prescribed<br/>
Tonics I concocted in my emeril legasse prime<br/>
You wanna try its not a wine<br/>
It’s acquired taste I describe as swallowing a shot of slime<br/>
Toxic and lot of guys vomit traumatized<br/>
Not surprised, psychedelics show you God inside not disguised<br/>
Tripping on the yacht that Willy Wonka rides<br/>
A nightmare to you is like nirvana for the shaman guide<br/>
Qualified thrive in demonic diabolic binds<br/>
Buddha Theravada Maharashi with a ganja shrine<br/>
Chronic with the crystals in the soil got it modified<br/>
Stronger than exotic hydroponic kind<br/>
Got it if you wanna buy, sour to the chocolate Thai<br/>
Whatever I don’t got in stock arrives when the flowers dry<br/>
Keep us in a garden where seeds don’t ever blossom<br/>
Cuz the bees that give them pollen just forgot fly<br/>
Chakra rise from sacram if you got a spine<br/>
33 vertebrae are levels that you gotta climb<br/>
Prana wise I'm Muhammad when personified<br/>
Annunaki, I jotted the gospels the Masonics hide<br/>
Got assigned a name, a word the word "god" implies<br/>
A word words cannot interpret cuz im not defined<br/>

### 10) King of the Jungle Lyrics

[Verse 1: Cambatta]<br/>
I remember when life was better<br/>
I remember like I been alive forever<br/>
I remember being born in abundance you’ll never measure<br/>
Predecessor from the epicenter the genetic Mecca<br/>
I’m a representer of the Medu neter<br/>
You dead if you never met her, the devil he never fed her<br/>
I protect her treasure then oppressors entered<br/>
Kemet was never desert do the rain dance make the weather wetter<br/>
A crown is a head antenna call me Imhotep the architect I’m clever<br/>
Break a temple down then put it back together<br/>
[Bridge: Cambatta]<br/>
I remember I was royalty<br/>
From the soil where the oil be<br/>
Never let the bigger man in me<br/>
Grow up from the little boy in me<br/>
Been a victim of my loyalty<br/>
Let my ego kill the joy in me<br/>
That’s what ended up destroying me<br/>
I forgot the lord anointed me<br/>
[Chorus: Cambatta]<br/>
I forgot that I was god, I forgot that I was free<br/>
I forgot that I was king of the jungle until I remembered I’m me<br/>
She forgot that she was God she forgot that she was free<br/>
She been stuck up in this slumber so long she forgot she was ever a Queen

### 11) Barmageddon Lyrics

[Verse]<br/>
If I open up my lungs I'mma fill 'em with smoke<br/>
If you open up your ears I'mma fill 'em with dope<br/>
But if I open up my palms and you don't fill 'em with dough<br/>
I'mma open up your mouth and take a shit in your throat<br/>
Billy The Goat, drippin' without sniffin' the coke<br/>
Grippin' a rope, climbin' up a slippery slope<br/>
Lift up and float, vision of a sinister ghost, invisible cloak<br/>
Hidden like a mystic occult<br/>
Gimme the toast, I'll kill 'em if a kiddie is groped<br/>
My future got a Billy in it like a Hillary joke<br/>
Givin' 'em hope, give 'em what a minister won't<br/>
I give 'em the map, they stranded on a Gilligan boat - Lost!<br/>
Never try, yet I always win, I don't ever lose<br/>
Only way I cannot prevail is if I try to fail<br/>
I am ?El?, Elohim, king Judah, lion male<br/>
Never lyin', Elijah in Zion in the highest realm<br/>
I rebelled, so then I was nailed, metal spike impaled<br/>
Godson, soul<br/>
Israelite<br/>
, in the sky it's hell<br/>
Seen it bright, inner side is fine, yet I'm blind as well<br/>
Got the book like I'm Eli and my Bible Braille<br/>
Exhale, then I inhale till I'm high as hell<br/>
Raise hell, till it's heaven's hight, you'll need a helicopter<br/>
Hellraiser, see a Satan<br/>
here, I'm a devil barber<br/>
Cut the horn, call me Hellboy, 'cause my head is altered<br/>
Devil, run! Go to Helen Hunt! I should get an Oscar<br/>
Helen Keller, heard a fat lady at the devil's opera<br/>
Slept with monsters underneath your bed, I'm under bed of monsters<br/>
Metal chopper was the first time I ever met a poppa'<br/>
Redenbacher<br/>
, kept a Tec and Glock in elementary locker<br/>
Head is larger, skull elongated like Kemetic fathers<br/>
Never conquered, the best evolvers, we dimension hoppers<br/>
Dennis Hopper, bring the war to worlds for the extra aqua<br/>
Kevin Kostner dancin' with the wolves, you ain't steppin' proper<br/>
Benihana, chop the ?Reddy Rock? up, then behead imposters<br/>
Weapon armour, feel like Ted Kaczynski in a leather bomber<br/>
Next to Batta any mortal human is a pet chihuahua<br/>
Textin' all the numbers in existence till I get Rihanna's<br/>
Sexin' on her, hope I get her pregnant with a second Batta<br/>

## The Holy Ghost III (16 December 2023)

### 2) Kanye’s Inferno Lyrics

[Verse 1]<br/>
Fuck swine, keep the money in the bloodline<br/>
We already did enough time<br/>
Never put a god above mine<br/>
Everybody deaf, dumb, blind<br/>
Mankind kinda unkind<br/>
Pull a gun on me, the gun died<br/>
Weed smellin' like a skunk died<br/>
Fungus is a fungi<br/>
When the plug drive, got a supply<br/>
You should come try<br/>
Cambatta in your junk drive, it's a drug crime<br/>
And it's so raw, I could cut mine<br/>
Like a soft-white in a lunch line<br/>
And it's still pure like a monk mind<br/>
In a uprise, I'm a young fly nigga so you know I run and jump high<br/>
I could touch sky<br/>
I could look into a dove's eye<br/>
Starin' in the sunshine, I don't blink one time<br/>
I was on a tough climb, made it up finе, now I'm doing just fine<br/>
On the upside, long (raining/rеigning) at the [?] level, shed a top (tier/tear) if I must cry<br/>
Daddy never knew his son [?]<br/>
Turn a battle to a blood[?]<br/>
Sippin' blood wine, tryna unwind in a trunk but I never drunk drive<br/>
In a Tesla, I just ?ride?<br/>
Black king but the skin gold like my flesh temple is a tuss shrine<br/>
Head shaped like an Anunnaki with my arms out, I'm an Ankh sign<br/>
Hang a (prophet/profit) on a plus sign<br/>
Blank check 'cause I'm unsigned<br/>
God handed me a lemon, turned it into Sprite, I just needed one line<br/>
Tapdancing to the drumline, punchline leave a shoe tongue-tied<br/>
My voice sound like Malcolm, Martin, Khalid if they all combined<br/>
I do everything in one try<br/>
Hand goes where the pen moves<br/>
Penpals with a dead dude<br/>
Grandmama made the best soup but I couldn't eat it 'cause I bend spoons<br/>
Take a tab, dab, then shroom<br/>
Needle in me like a thread spool<br/>
Just a few of the essentials if you wanna get me in a Zen mood<br/>
Calculated in my next move<br/>
Retire undefeated, then lose<br/>
Footprints that I left huge, all ten toes need ten shoes<br/>

## The Holy Ghost (15 December 2017)

### 1) Black Magic Lyrics

I came from the Nile Valley<br/>
It's bitter sweet, I smile sadly<br/>
Truth rarely seen like child's daddies<br/>
I'm Imhotep, I style flashy<br/>
Regarded highly I'm Selassie<br/>
As time is passing tribes are clashing<br/>
I know the ledge, I grow my dreads<br/>
My queens two open legs has golden eggs; I'm hatched<br/>
Nine months had to hold my breath<br/>
Now i dream so heavy that i broke the bed<br/>
Provoke the feds that slaughtered the son<br/>
12's get the 4 to 5 like a quarter to 1<br/>
The war has begun<br/>
Latin for son<br/>
The soul and melinates get more of the sun<br/>
We the fortunate ones<br/>
Got the God in the womb, the Lord in my cum and (amour / a moor) means love<br/>
Death is the source that im from<br/>
Everything that they do we have already done<br/>
Self taught<br/>
Mine ice and melt salt<br/>
Mind high price, I write and sell thought<br/>
I felt cloth<br/>
Ahkenakin cotton shopping<br/>
Aquaponic chronic options<br/>
Botanizing pot concoctions<br/>
Earths a thot, her twat is rotten<br/>
Knowledge of my eye forgotten<br/>
Watch the conscious sovereign doctrine<br/>
Not dishonest profit goblins<br/>
Boxing out the box I'm boxed in

## Tupac Murder Confession (20 Sept 2016)

### 1) Tupac Murder Confession Lyrics

<br/>
To be the best you gotta beat the best<br/>
To be a God, then you must be the reason for their breath<br/>
Or why they meet with death<br/>
You can only live forever if you die<br/>
And you can only gain it all when you lose it and you have nothing left<br/>
To sacrifice is to take a life for a greater purpose<br/>
Sometimes a martyr doesn't know that it's his day for service<br/>
To kill a king you make him infinite<br/>
And I just represent the sword of his deliverance<br/>
I'm confessing to the murder of 2Pac Shakur<br/>
I started the brawl in that lobby hall<br/>
I followed his car til it stopped that's when I popped the Glock and shot his door<br/>
September 7th's when I shocked you all<br/>
But let me tell you how I got invovled<br/>
I remember when I got the call it It was ____<br/>
He said he need another problem solved<br/>
Last one was easy, after this one they gonna call us Gods<br/>
On Allah, getting caught's not a thought<br/>
Cops and lawyers on the squad<br/>
, He'll pay me a million dollars large<br/>
I responded with who's the target mark?<br/>
But not on the horn, let's discuss its all tommorrow<br/>
Next day, shopping mall, parking lot, got in car<br/>
Hoping we could plot it all, but it all was odd<br/>
And after a long awkward pause....<br/>
He said "Pac," I said who? He said "Pac!"<br/>
I said how? He said "shot" I said when?<br/>
He said "soon" I said cool<br/>
Then he said its all depending on you<br/>
That was one day before the seventh day of June<br/>
Same week "Hit Em Up" was new, I knew what I would do<br/>
I'ma play the red against the blue<br/>
Deceptive in my moves perceptive of the moons<br/>
Patient, waited til September for the clue<br/>
Pac will be in Vegas with his henchman and his crew<br/>
I'm striking preemptively like specialists would do<br/>
Met a nigga Zip, led me to a crip<br/>
Keffe D, said he'll help me with the hit for a split<br/>
He'll even get the whip and won't snitch<br/>
Told him meet me at the strip, stick to the script don't slip<br/>
I stole the Glock from a cop that stole the Glock from a box<br/>
From out of an evidence locker that's locked<br/>
Pac already shot two cops<br/>
So it make senses that cops went and shot 2Pac or maybe not<br/>
Death was dodged when Pac had his necklace robbed at Quad<br/>
But God said finish off the job<br/>
Remember it like yesterday, in my head it plays over like broken records play<br/>
Sabbath on the seventh day<br/>
Moon was in a crescent shape<br/>
Met up at the MGM entrance way<br/>
Estimate the time around 7-8<br/>
Set a fake motive give the Feds a case<br/>
Jump him when he steps this way, try to make his necklace break<br/>
Only minutes after the Tyson fight<br/>
Bruce Seldon ain't the only nigga getting iron mike'd<br/>
Keffe's brother Baby Lane tried to take his chain<br/>
Pac hit the nigga hard enough to shake his brain<br/>
I hit Suge Knight with a punch harder<br/>
Than the one he caught in LA by Greg<br/>
Then I fled the scene to the white Cadillac<br/>
T Brown, Keffe D, Lane got the strap in back<br/>
Young nigga pass me that, soon as Pac left<br/>
We was on him like a taxi cab driven by that Travis cat<br/>
Hands on the wheel like he trying to do the cabbage patch<br/>
Pac stopped at the Luxor where his bags was at<br/>
Switched shirts to the same jersey that he wore<br/>
In the "How Do You Want It" joint, so I'll be sure to ask him that<br/>
Got a tip he's headed to the 662 club<br/>
Soon as he moved we pursued him<br/>
Red light ahead, on the right side how we pulled up<br/>
Same time on the left side was these two sluts<br/>
Now that they're distracted it's the perfect time to shoot guns<br/>
Stretch on my new gloves, roll the window down I'm ready<br/>
Aim it at their black 750 arm strong and steady<br/>
Let off one shot for every song on the Makaveli<br/>
(Blaat! Blaat! Blaat!) I'm sorry for your mom Afeni<br/>
(Blaat! Blaat! Blaat!) I like your aunt Assata heavy<br/>
(Blaat! Blaat! Blaat!) If you live I hope you go to Cuba<br/>
(Blaat! Blaat! Blaat!) I hope they got my million dollars ready<br/>
Grazed Suge's head to show him he ain't God of any<br/>
Skurt! Then we pulled off like I'm Andretti<br/>
Took a quick right passed the Glock to Keffe D<br/>
Hurry to the club, give it to an undercover cop named Reggie<br/>
First drop me at the telly where I laid low<br/>
A little later hit the pay phone<br/>
Called _____ told him that I got him, where the pesos?<br/>
He told me he ain't dead yet, they still trying to save holmes<br/>
If he don't die then the bank closed<br/>
I hung up mad, damn! Pac got them slave bones!<br/>
Somehow his body eat the bullets when I spray chrome<br/>
Needed better aim though, 6 more days for him to fade slow<br/>
Over that time I went insane though<br/>
Never got the gold at the ending of the rainbow<br/>
Connected all the angles, like his gold chain rope<br/>
Euphanasia pendant on it, Death of an Angel<br/>
Serpent getting wrestled on it, search and see the message on it<br/>
Perfectly connecting all it, everything occurring got a 7 on it<br/>
He was 25 that's  7<br/>
Died at 4:03 thats 7<br/>
I shot him on the 7th, three numbers everybody out in Vegas wanted<br/>
It's like someone in heaven trying to send a warning<br/>
2Pac reversed is caput or destroyed<br/>
Shakur flipped around spells ruckus which is noise<br/>
Noise when destroyed is eternal silence<br/>
Deaf and death sound like the same word recited<br/>
Are you convinced yet?<br/>
Blood sacrifice a goat wrong and get hexed<br/>
I might've conjured too much power for this thin chest<br/>
Safe to say the past twenty years I been stressed<br/>
2Pac Amaru was an Incan King<br/>
That was beheaded cuz he fought to keep his people free<br/>
Probably by a nigga just as weak as me<br/>
I killed the cub of a mother Panther that speaks to me<br/>
She said the day you die your soul will be released to me<br/>
I know it's you that stuck that diseased needle in Eazy E!<br/>
The karmas eating me!<br/>
And I keep another secret deep<br/>
I'm confessing to the murder of Christopher Wallace<br/>
It was me squeezing heat at his GMC!<br/>

## Smoke & Mirrors: DMT (Definitive Metagod Trilogy) (2016)

### 1) DMT Lyrics

[Intro: Terence McKenna]<br/>
I’ve never seen it hit anybody quite as hard as it hit me but I was transformed<br/>
It was then and I will say it still is now; it is pure 100% magic!<br/>
It’s not a drug, it’s an event<br/>
It’s not something that you do; it’s something that happens to you<br/>
People come out of it saying, what happened?<br/>
[Verse 1: Cambatta]<br/>
What is DMT?!<br/>
Dimensional Mind Travel, the Devil Might Trap you<br/>
It used to be a Dogon Mapping Tool<br/>
How the Dark Man Thrived, Deceptive Manipulation of Time<br/>
It's a Dope Magic Telescope<br/>
The Doorway to Many Things<br/>
So I Do Major Tokes 'til I Damage My Throat<br/>
I'm a Dead Man Talking that Died Maybe Twice<br/>
From a gram not your Dad Mother's Type<br/>
Get my Damn Music Tight 'fore I Dial My Troups<br/>
And we Demonstrate Melee Tonight<br/>
And I Don't Make Truces<br/>
I'm just my Doing My Thing I Decide what My Truth is<br/>
Dependent on Melodic Tones<br/>
Descendant of the Mayan Throne<br/>
Digging Meticulously for Treasure<br/>
Hoping I Define my Texture

### 2) The Womb Lyrics

[Intro: Cambatta]<br/>
The womb, (yeah)<br/>
Scientifically referred to as the womb-man's uterus, ('Batta)<br/>
Or the place that your current human experience initiated it's first nine months of three dimensional development, (smoke)<br/>
Some say that your spirit or your light transmits into your brain's pineal gland in the thirteenth week of gestation<br/>
Thirteen being the highest of the Sephira<br/>
The beginning & the end of the cycle<br/>
This is not your first time here<br/>
(You will never die)<br/>
Can you see now?<br/>
(You will never die)<br/>
Can you see now?!<br/>
Welcome back (to the womb)<br/>
[Chorus: Cambatta]<br/>
I'm stuck in this womb<br/>
Tryna find my way out<br/>
But I don't have a clue<br/>
In midst of of this womb-man<br/>
9 months of darkness<br/>
'Til finally break through<br/>
Now I'm stuck up in this room<br/>
Tryna find my way back<br/>
Back inside of that womb<br/>
In the midst of this womb-man<br/>
My life is of darkness<br/>
'Til I finally break through

### 3) God On Crack (S&M:DMT) Lyrics

[Intro: Cambatta]<br/>
I'm just a fuckin' fiend in a long-ass dream<br/>
So fuck you, and everything in between<br/>
[Verse 1: Cambatta]<br/>
I'm sleeping in the bed that they conceived me in<br/>
Checking in the hotel they shot King up in<br/>
The podium they shot X where I preach to them<br/>
The opium that got Basquiat's, what I'm chiefing with<br/>
I'm fucking in that manger they birthed Jesus in<br/>
Climax, leave it in, never shall we meet again<br/>
I'm drinking out that cup that Christ bleeding in<br/>
Cooking crack in the pot that the rich man's peeing in<br/>
I'm cumming in the womb that you came up out<br/>
I came up in before you even came about<br/>
My sperm saw the egg and had to change its route<br/>
Crack baby; I'm just lucky that I made it out<br/>
I take the crack up out the water and strain it out<br/>
Crack schemes make the rap fiends rave and shout<br/>
I'm swimming in an ocean full of slave bones<br/>
I'm a hostage of the giver of the bank loans<br/>
Every time I leave my porch, I should've stayed home<br/>
I get that liquor in my system and brake, bones<br/>
[Chorus: Cambatta]<br/>
I promise you don't want it with the 'Batta man<br/>
I promise you don't want it with the 'Batta man<br/>
I never felt the embrace of my father's hand<br/>
That's why that thang thang is braced up in 'Batta's hand<br/>
All my life I get so high that I don't wanna land<br/>
What would you do if your God told you that his God is Cam'?

### 4) Rebirth of the Crack Baby Lyrics

I'm the 'Batta man, human contraband<br/>
Cause I'm illegal like a bird in a doctor's hand<br/>
I saw my sonogram, and I appeared to be centrifugally spinning<br/>
In the same position how Sonic ran<br/>
Daddy not a Super Sonic fan, fuck a glove<br/>
Momma want a ring on her knuckles like what's in Sonic's hands<br/>
Pussy is his promised land<br/>
Mecca is the black box, got 'em on his knees like Islamic man Prayed to God and got a Cam and placed him in the center<br/>
Of placenta ff the place that you enter<br/>
To the hole like I play center<br/>
Layed up as my body and my face render graced is the great scepter<br/>
Incubated in a hydroponic grow box<br/>
With radiated glow rocks then closed up with a bolt lock<br/>
My birth certificate had no pops<br/>
It's kinda like I'm baby Christ but instead of a manger it's a dope spot<br/>
From a place were you don't call cops<br/>
They cooking base inside the basement but the door ain't locked<br/>
I was just a tot when I walked in and I saw them pots<br/>
Boiling hot<br/>
Weed as loud as Haitians in the barber shop<br/>
Patrons come to bargain shop the place to get that raw and rock<br/>
Take these vivid memories and place them in my story plot<br/>
Witnessing the birth of black Jason and the Argonauts<br/>
Armed and got a army set up bases on a foreign block corners pop<br/>
My life story's a John Singleton movie<br/>
Rock slinging and Uzi's, pot chiefing and looseys<br/>
Substitute me and make Pras leave out the Fugees<br/>
Am I 'Pac or am I Big in that car seat in the Coogi<br/>
If it means I'll be endowed with the God features then shoot me<br/>
What? Hold my car keys and my jewelry<br/>
I'll concuss you , then I'll spit out a hawk heave and a loogey<br/>
On your baby girl head like I'm flea in that movie<br/>
It's killa season, getting even, the pistol squeezing<br/>
On these simple heathens, shipping bricks up to different regions<br/>
Like its Christmas season, committing treason<br/>
Prison system sneaking on me like a ninja creeping<br/>
So I Assassin Creed them<br/>
What if when you're dying on your deathbed<br/>
The secret to revitalizing life is being breast fed<br/>
Before that moment that I'm dead<br/>
I'll fuck so many virgins when I'm resurrected<br/>
I'll wake up in a red bed<br/>
I encapsulate the universe sonically<br/>
My physiology represents the dichotomy<br/>
I think I now overstand the idolatry<br/>
If I'm dollar tree you, you climb on to me<br/>
You take fruit from me, you hang noose from me<br/>
If I'm dollar tree, you try chopping me<br/>
I wish a nigga wood, I'll pop the trunk<br/>
There's more bite than bark in me<br/>
I force the belief and all them addicts fall from me<br/>

### 5) When Gods Use Guns (S&M:DMT) Lyrics

This is what happens when Gods use guns<br/>
Batta<br/>
Smoke!<br/>
I'm a Jehovah's Witness with no arms<br/>
When It come to that dough I'ma head knock<br/>
I hit the ground running how that whip work<br/>
Car flawless speeding through Bed Rock<br/>
I'm Rafiki in a dashiki<br/>
Sex simba, I mufasa<br/>
Brother lion to the king he a coon I'ma Ta Ta<br/>
Scar him, swallow slugs like Pumba<br/>
When I'm stressed out I do a woosah<br/>
I'll flip a dub to a bird like the Wu sign<br/>
Them little piggies killed my dad out in Tucson<br/>
They ain't know that nigga's son was a wolf God<br/>
I burst shotties<br/>
Bullet holes O.D. in the middle of your body like the word body<br/>
This a purge party<br/>
I'ma bring the can in like its BYOB but I thirst hardly<br/>
Ima burn Marley Over your body<br/>
Puff, drop ash on tee Like Irv Gotti<br/>
Ink murder like cephalopod poison<br/>
My voice is just weaponized noises, Batta<br/>
I was born on July 21st<br/>
If I shoot you and you live you a cancer survivor<br/>
I'll burn a Mac in your back<br/>
Like the dead black comedian's ambulance driver<br/>
I screw ratchet hoes for the nut<br/>
And then bolt to twist up please hand me the pliers<br/>
You got a sack? I'ma make you all red<br/>
Put a cap to your head like Santa's attire<br/>
The Devil's just God in a ski mask<br/>
Leave you stiff for the base like freeze tag<br/>
Red dots when I squeeze mags<br/>
Batta turn a pale face to a fucking Japanese flag<br/>
That shit sound Mike Tyson on a speed bag<br/>
Bbbrbrbrbbrbrbbrbrbrb you can keep that<br/>
Shots rectum, lick lick they eat ass<br/>
Your red blood looks so pretty on green grass<br/>
I'm 'bout dollars I'm cross seas like cent signs<br/>
I send shots across heads like lent time<br/>
My Trigger is a clitoris I hit a G spot<br/>
Anytime my finger get to flicking it's a sex crime<br/>
I'm circumcised<br/>
But I'm 'bout to have my foreskin re-attached so I can fit the work inside<br/>
Or I put a zipper on my scrotum<br/>
The cops come I fill it up with coka<br/>
I'll take a hit of acid to the face like a misbehaved Arab woman<br/>
Crush a couple qualudes in a pack of puddin<br/>
I wait til she go to sleep then I smash her puss in<br/>
Hit it so good she wake up she glad she took it<br/>
Cops blasting bullets<br/>
They can give black man a red neck, nigga that's an afro mullet<br/>
My plug is like a couch cuz he has the kush in<br/>
But he don't let me in the kitchen when that crack is cooking<br/>
I want a Bugatti like Mickey Ward's fans<br/>
My wrist game so strong like I got 4 hands<br/>
I'll restructure the floor plan of the Lord's land<br/>
If I have to waste another day as a poor man<br/>
Bitch I'm too lit<br/>
I'ma dilate my nostrils and hit this 8 ball like a pool stick<br/>
Sniff sniff snort ooh sniff<br/>
Whip whip whip, I need a new wrist<br/>
The deuce spit at you dudes with loose lips<br/>
Then I jet with a goon dough like Bruce did<br/>
Fuck a Consequence no Q-Tip<br/>
Young X boomer to your back I'm a new pit<br/>
I'm a stoner like a caveman<br/>
I can hold a blunt and light it with the same hand<br/>
I can break down glass and make sand<br/>
I can see the words in the numbers like Rain Man<br/>
When you pray you end it with an amen<br/>
When God pray he end it an A-Cam<br/>
I can stare straight at the sun with no rayban<br/>
All that bull shit in the Bible's a straight scam<br/>
Generate, Operate, Destroy<br/>
My job description on this planet I'm employ<br/>
If Eve ate the apple I'm a fucking android<br/>
Satan whispered in my ear when I was just a little boy<br/>
Told me step out from the silence get adjusted to the noise<br/>
Kill them psychologically like i was studying with Freud<br/>
Nigga they stuck me in a void<br/>
Gods grab guns when they're annoyed

### 6) Hallucinate Lyrics

[Chorus: Cambatta]<br/>
I think I'm hallucinating (ahh yeah)<br/>
I think I'm hallucinating<br/>
I must be hallucinating<br/>
Yeah, I'm hallucinating<br/>
Hallucinate<br/>
Hallucinate<br/>
Hallucinate<br/>
(x2)<br/>
[Verse 1: Cambatta]<br/>
Hallucinate, I'm truly baked<br/>
These 'shrooms are great<br/>
The few I ate got me viewing space<br/>
In cubic shapes<br/>
Everything I see got a human face<br/>
Did the room just shake?<br/>
I could close my eyes and illuminate<br/>
From the<br/>
triple black to a fluid state<br/>
I been losing weight I got moves to makes<br/>
I got rules to break<br/>
And I don't believe that my dookey stank<br/>
I got Gucci skates, I rock super capes<br/>
I'm like Tunechi babe<br/>
Cut the bird,<br/>
I got goose to rape<br/>
I put roofie in juice I drank<br/>
And I'm so high that I'm through the gate<br/>
Between truth and fake<br/>
Red or blue pill, I choose my fate<br/>
Smoke and fuck, am I Snoop or Drake?<br/>
I can see error In my future ways<br/>
When I Lucy take<br/>
Got me running home<br/>
I'mma pitch the ball, I Babe Ruth the base<br/>
I'mma rise early, make a rooster wake<br/>
I be getting trippy like I'm Juicy J<br/>
So confused and dazed<br/>
<br/>

### 7) Too Loud Lyrics<br/>

<br/>
Smoking smoking smoking smoking<br/>
All a nigga do now<br/>
[Chorus]<br/>
Oh now, smoking that too loud<br/>
Smoke is in the air I don't care if it's too loud<br/>
Only want it if it's too loud<br/>
Fucking yo bitch, 'til the neighbors tell me that hoe too loud<br/>
Oh now, Black and I'm too proud<br/>
Smoking 2 pounds, got me feeling like I'm Snoop now<br/>
Oh now, that might be too loud<br/>
Oh now, smoking that too loud<br/>
[Verse 1]<br/>
It's Batta man, and you know my whole crew wild<br/>
I setup up the trap, like I'm  home alone inside a new house<br/>
I know I fronted you a day ago but it's due now<br/>
You don't pay me I'ma blaze steel, Juice style<br/>
Bought a new coat it's a single double triple goose down<br/>
If you gotta pack a few rounds it'll help when coppers patting you down<br/>
Oh no no, look at all the hoes I screw now<br/>
Never use a rubber so every time I fuck I end up making a new child<br/>
Baby mama got the cracker on me getting sued now<br/>
What's a nigga gonna do now? Move pounds<br/>
Even sell it on the school grounds<br/>
Fuck an education make the money let a Jew count

### 8) Trippin Balls Lyrics

Hey thats not a blunt thats a unicorn penis<br/>
I'm tripping I'm a motherfuckin genius<br/>
I'll buy a gram, zap myself with a shrink machine and smoke for life<br/>
Sleep in a stripper's vagina what a cozy night<br/>
This reminds me of my mother's womb<br/>
Warm, welcome to the mind of a rapper that sees drugs as food<br/>
[Chorus]<br/>
The acid and the shrooms got me tripping balls<br/>
The DMT fumes got me tripping balls<br/>
I'm going so deep I might trip and fall<br/>
I live life by a set of these specific laws<br/>
Get money find drugs trip [X4]<br/>
[Verse1]<br/>
Woot woot, shoot the deuce deuce<br/>
Through the roof of a goof troop<br/>
You a fruit loop, poop poop on ya new boots<br/>
Vroom vroom in the blue coupe soowoo Mewtwo with a new move oh<br/>
Weed smoke by the kilo cuz I need dough<br/>
Repo by the peep hole<br/>
Speak low reload what the heat hold<br/>
Keep low squeeze blow leave holes bleed slow negro<br/>
3'4 still dunk from the free throw<br/>
Please know the libido's on beast mode<br/>
Speedos so the hoe see I'm a dingo<br/>
Cheat code on the beat flow like a hero<br/>
And if she greet me with deep throat I'm a G on a speed boat<br/>
Back to the, hood unlimited chicken wings for my people<br/>
Smoke

### 9) Holy Ghost/Sun Of Set Lyrics

[Verse 1 "Holy Ghost"]<br/>
If a nigga wanna brawl<br/>
Then a nigga wanna brawl<br/>
I'ma hit em in the jaw, then I sit him on the floor<br/>
While the video is on and I'm twittering it all<br/>
I was Living in the fog now I'm penning all these bars<br/>
In my head it's a collage, you ain't never know Connecticut was hard<br/>
'Til I went and got the hill and ville invovled<br/>
I smell, I smell, I smell pussy<br/>
One shot will have you ushy gushy<br/>
When I talk you make cuckoo sound<br/>
God is racist for making doodoo brown<br/>
My penis needs attention, my testicles are blue<br/>
I think we need an intervention with some sex on the menu<br/>
I just wanna do god invented me to do<br/>
And then I entered her in less then 20 seconds I was through<br/>
[Chorus]<br/>
I caught the Holy Ghost<br/>
I caught the Holy Ghost<br/>
I caught the Holy Ghost<br/>
Yeah!<br/>
I fucked around<br/>
And caught the Holy Ghost<br/>
I caught the Holy Ghost<br/>
I caught the Holy Ghost<br/>
Yeah!<br/>

### 10) Lawdamercy Lyrics

[Verse 1]<br/>
I'm tight roping the Grand Canyon I'm high as fuck<br/>
My pipes holding a gram damn it I'm tryna puff<br/>
A psycho I'm the Van Damme of this rhyming stuff<br/>
It's my flow that advanced planets are tryna clutch<br/>
So throw your diamonds up, but where is your pride?<br/>
Know how many tribes and innocent lives in Africa died so you can be shining up?<br/>
But still you at jeweler buying stuff cuz when you shining hoes is lining up<br/>
See I don't bother with designers much, I can't afford to pay the price for lust<br/>
Light the Dutch, I'll be smoking til i bite the dust<br/>
High as heaven telling Christ what up<br/>
I be blessing every mic I touch, tiger punch!<br/>
Ken and Ryu, Guile Bison punk, genocide in every rhyme I bust<br/>
The state of Florida got my license fucked I rather stay at home then ride the bus<br/>
The greatest hustler ever I'm a mighty con<br/>
You my gayest customer ever, you a maricon<br/>
I write a song and ignite a bomb I’m a silent fire arm<br/>
Inside the palm of a child soldier reciting psalms<br/>
Amen<br/>
Lawdamercy<br/>
When I die just bury me In a Jordan jersey<br/>
[Verse 2]<br/>

### 11) Marcus Barvey Lyrics

Marcus Barvey<br/>
Selassie I, Amen Ra Batta's God<br/>
Shalom Shabbat, Jah Alla, Dali Lam poppa<br/>
Arm and hammer make ya soft body rock<br/>
Automaton drop a bomb get my Sovereign on<br/>
I go to sleep inside a cryogenic chamber bed<br/>
Preserve my flesh so I don't die before I make this bread<br/>
I'll let dust from the angel spread through my crazy head<br/>
Then lick the coke off a razor's edge and escape the Feds<br/>
I doggy paddle in the sea and make a tidal wave<br/>
I back stroke in a circle and cause a whirlpool<br/>
My current's strong enough to set off a lightning chain fire rain<br/>
My blow can derail an iron train<br/>
I created every woman with my rib bone<br/>
I'm absorbing radiation with my skin tone<br/>
I'm just a stream of thought that my skin holds<br/>
And you are not you you're just him cloned<br/>
Defying physics like a giant midget<br/>
My Favorite measurement of time is minutes<br/>
Cuz all I need is 60 and this world is hours<br/>
Every relic that you find in kemet I invented<br/>
I warp space so dark matter I'm trying to bend it<br/>
If knowledge was good as cash how would you spend it?<br/>
Africa diaspora I'm dying in it<br/>
Africa diaspora I'm dying in it<br/>
Cover mother earth's skin with my genetic make up<br/>
I lash out but never mess her face up<br/>
Batta

### 12) Ghost In The Machine (Power of God) Lyrics

[Intro]<br/>
I die when I go to sleep everyday is birth<br/>
If money rules the world what's your worth?<br/>
[Hook]<br/>
If you ain't got the power then the world won't believe you<br/>
Trying to do good, do a little evil<br/>
Cops don't see you then it's legal<br/>
I do this for my people, I'll see you when I see you<br/>
You ain't got power then the world won't believe you<br/>
Trying to do good, do a little evil<br/>
Cops don't see you then it's legal<br/>
I do this for my people, see you when I see you<br/>
[Verse]<br/>
From crack smokers to black homeless<br/>
With rats roaches I'm freeing my people I'm black Moses<br/>
I split the sea so you see that the path opens<br/>
If you don't see the evil that leads you, you lack focus<br/>
I keep the heat in the seat of the jeep<br/>
Creep til I see the police bleeding, them demons that made my dad soulless<br/>
Bad omens got me backbone-less<br/>
The cash loans of upperclass owns us<br/>
I strike back like bad Shaft with a gat holster<br/>
But fuck a badge I'm a black soldier, Black Panther, black cobra, rap's Yoda<br/>
Black Hebrew, no pork at the Passover<br/>
Lyrics passed Hova but I'm still getting passed over<br/>
Rise from the dead in a cave push passed boulders<br/>
The New Testament I'm passed Torah<br/>
Hold up, Judas Priest that uses speech to rule the weak<br/>
Religion is the tool I reap...with<br/>
There's 12 levels of a ruler's reach<br/>
The thirteenth is not viewed or seen in full mystique<br/>
With the puns I am too succinct<br/>
Like Cuban Link the rope used to noose the streets<br/>
For the R.E.S.P.E.C.T. see me<br/>
In the C.T. streets with E.B.T. on me<br/>
Got the heat on me like CP3 from 3<br/>
Gold jewelry like CP3 oh sheesh<br/>
Pay a fiend get the TV free<br/>
Thats throwback like T.B.T<br/>
Hoes bring me free bread, pussy leak yeast for cheap<br/>
Bars on lock I'm D.O.C<br/>
I'm the D.O.G. in mirror I am G.O.D<br/>
Doc King fuck C.O.P.'s<br/>
Doc Brown don't T.I. me<br/>
Do time for the machine document me<br/>
Dot com triple the dub then dot Ghandi<br/>
Me hot I be dot com click pops up me<br/>
The god M.C. I'm he<br/>
Inner telescope sinners get awoke<br/>
Piff is getting smoked think I need to get a second throat<br/>
Sick of jealous folk picking telling jokes, pistols sending note<br/>
Box em up, shots licking envelope, pen a quote<br/>
Hear the beat with a stethoscope and check the pulse<br/>
Defibrillate with an extra bolt your chest will jolt<br/>
This like the greatest shit I ever wrote<br/>
I ain't get awake I been awoke<br/>
When in Rome I behead a pope<br/>
I stick a needle in my temple off the head I'm dope<br/>
Get a fix never broke<br/>
Blacks are now gentrified thugs<br/>
Food is just weaponized drugs, kettle fried crud<br/>
Crack is still a ghetto wide flood<br/>
Sinning all seven I does, tempted by lust<br/>
Fucking so I never find love<br/>
Cops tryna empty my blood all they get is my snub<br/>
They killing all the fathers, so momma gotta raise us<br/>
Why you think we got these feminized sons, Smoke!<br/>
And we ain't hungry we just eating for the taste<br/>
We just fucking for the nut so the semen go to waste<br/>
We just spraying black babies like our penis was a jake<br/>
What if your momma told you that she conceived you by mistake<br/>
You call me Nigga to my face racist<br/>
And I'll be busting off the metal like Forest Gump in them leg braces<br/>
I change paces when the game changes<br/>
Then I'll assassinate your leader and remain nameless for payments

### 13) Spark of Divinity II (Perfect Poetree) Lyrics

It's like the sweetest thing I've even known<br/>
Since a fetus thinking belly's home<br/>
Blind and still I've seen the kingdom heaven holds<br/>
It's hidden deep in each and every soul<br/>
You can't defeat it if you let it roam<br/>
And though I need it I still let it go<br/>
I think that freedom sings in baritone<br/>
Adjust your frequency and hear the ohm<br/>
Quantum entanglement I'm here to comb<br/>
Mind to brain is Internet to phone<br/>
I think I hear the music inside of me<br/>
Is this a skeleton or a scale of tone?<br/>
Ironically her ear rings are gold herringbone<br/>
Medu Neter I can hear her moan<br/>
Every time we bury bone inside her<br/>
Death is sex to globe<br/>
Life's a vacation and death is home<br/>
Your body's property you never own<br/>
But still I keep it fresher than the fruits on Dr. Sebi's stove<br/>
Some endeavors should be left alone<br/>
You may see the hero in the methadone<br/>
Med usa getting stoned<br/>
Stimulate my psychedelic pleasure zone<br/>
Fear the pheromones when I'm Pharoah mode<br/>
Trace my DNA to a Kemetic throne<br/>
I'm filling up my mental with the lesser knowns<br/>
And hateful eyes create stares that I step up on<br/>
The heart inside my chest is gold<br/>
My head is blown like Kobe fro back with Eddie jones<br/>
As hoes exit me and my exes do the X and O's<br/>
Her Levi's are like the levys to the heavy flow<br/>
Of genetic clones from the testicle<br/>
I took a slow walk down forever's road<br/>
And ended up somewhere between a rap and a Pleasant Poem<br/>
Moonwalk Michael Jack, Joe Pesci flow<br/>
Fire off the head like M.J. with the Pepsi though<br/>
How much truth does your legend hold?<br/>
What if heaven's hot and hell is cold<br/>
I catch a shark with no worm at the end of pole<br/>
Master of the bate this is sex alone

### 14) Blessing From God Lyrics

[Intro]<br/>
As I lay me down to sleep I pray to God I live<br/>
Through all the sinning, women, pitching bricks and mixing different shit to trip and binge<br/>
All these metaphors I see in life while hell is spreading dark at speed of light<br/>
Am I just numbing in life or getting one with Christ I guess it's me too decide<br/>
[Verse 1]<br/>
I remember thinking heaven was up in the clouds<br/>
Guess it was true 'cause the only time I get to heaven is puffing that loud<br/>
Got to the fountain of youth but it got a sign that say no coloreds allowed<br/>
I give a fuck what anybody think of me long as my mother is proud<br/>
I don't know what I'ma do, ever since I took them shrooms<br/>
I see the world in a whole different microscope like it broaden my view<br/>
Mary is getting abused, Bishop just gave me the juice<br/>
Why is that the most illegal things on this earth are what make us amused<br/>
[Chorus]<br/>
If you breathing right now it's a blessing from God<br/>
If you hear me right now it's a seeing from God<br/>
If you cheifing right now it's a blessing from God<br/>
'Til you see this you will never evolve<br/>
Put love in your heart and you'll better the odds<br/>
And make sure you pick when destiny calls<br/>
[Verse 2]<br/>
Anywhere I go I feel like I'm king of that biotch<br/>
Take it infinity beyond so Ima be great if it takes me an eon<br/>
Walking around with my gi on Mayweather when I'm pissed I'm the champ peon<br/>
Beat a cheetah in a 300 meters my feet are so endale E.I<br/>
I don't know what I'ma do, ever since I took them shrooms<br/>
I feel becoming a God is something I should actual try and pursue<br/>
Never rely on a fool, knowledge is my only tool<br/>
My purpose in life is to become the greatest rap artist that I ever knew

### 15) Something Ain’t Right Lyrics

Something ain't right<br/>
I grew up in a neighborhood<br/>
Where everybody's mother got a problem with that pipe<br/>
Something ain't right<br/>
I grew up in a neighborhood<br/>
Where everybody's father figure Ain't nowhere in sight<br/>
Something ain't right, Lord<br/>
How are you my Father when they tell me that your only son is white<br/>
I grew up in a paradigm where colored people kneeling on they knee<br/>
To get the worshipping a cracker named Christ<br/>
Something ain't right<br/>
How I'm supposed to learn to be a husband<br/>
When I've never seen my mother as a wife<br/>
Something ain't right<br/>
How I'm supposed to ever be a daddy<br/>
When I had to teach myself to ride a bike<br/>
Something ain't right, Lord<br/>
The only way I know to get this dough<br/>
Is with a rock or with a mic<br/>
Grammy had to empty out her pension just to make sure we had heat<br/>
And we had food and we had clothes and we had lights<br/>
Something ain't right<br/>
Every time I see a flashing redand blue light<br/>
I be fearing for my life<br/>
Something ain't right<br/>
God forbid there ever be a war<br/>
I hope my brothers and my sisters can unite<br/>
Something ain't right, Lord<br/>
I'm working to live<br/>
And I'm living to work til I die<br/>
The government manipulates your mind so they control and tell you every thing you like<br/>
And base your history on lies<br/>
Something ain't right<br/>
They telling all our women they ain't pretty<br/>
Unless they at a certain weight and certain height<br/>
Something ain't right<br/>
They telling all our women they ain't pretty if they dark<br/>
And you look better if you light<br/>
Something ain't right, Lord<br/>
They scandalizing sex<br/>
And make us hate the the way we look and feel inside<br/>
Every time I gaze into the mirror I'm just looking for my flaws instead loving what i see because it's mine<br/>

### 16) The Shaman Lyrics

[Verse 1]<br/>
I wake up like yesterday gave birth to me<br/>
And I live like every day is the first for me<br/>
If I die just listen to this<br/>
I’ll be living through the words in every verse<br/>
That you heard from me<br/>
I philosophy<br/>
I have a theory on metaphysics that haunts my mind<br/>
Let me try to explain<br/>
See my being is being contained<br/>
So what you seeing isn’t me, it's just something my being be in<br/>
See I’m really the soul that my body keeps in<br/>
The energy that you only feel when I’m speakin’<br/>
My physical features are just features<br/>
My mouth is no different than speakers<br/>
My eyes are like cameras<br/>
Ears are like microphones, and it gets deeper<br/>
See what if when you die you really waking up<br/>
And what you thought was your life is a dream<br/>
And you made it up?<br/>
I think about the power of the human brain<br/>
Mother Nature made birds and we made planes<br/>
Fish have gills, we made scuba gear<br/>
The future’s near, just think about what we doing here<br/>
What’s the definition of a god?<br/>
Creator, omnipotent power that sees all<br/>
We capable of all three, I mean really though<br/>
With one click of a button I could see any ho<br/>
With one click of a button I could learn anything<br/>
If knowledge is power than why ain’t I already king?<br/>
I dedicate this to the smart niggas<br/>
And loved ones that aren’t with us

### 17) Escape From The Womb Lyrics

What does it mean to escape the womb?<br/>
Earth is just seed in an even bigger womb ('Batta)<br/>
What is life? (Smoke, yeah)<br/>
How do you define something that you never truly understand?<br/>
It's all in my mind, all in my mind<br/>
It's all in my mind, all in my mind<br/>
It's all in my mind, all in my mind<br/>
It's all in my mi-i-ind<br/>
It's all in my dream, all in my dream<br/>
All in my dream, all in my dream<br/>
All in my dream, all in my dream<br/>
All in my drea-ee-eam<br/>
I wasn't born by a rock and a hard place<br/>
I was born by a rock of that hard base<br/>
Everyday there was a murder and a car chase<br/>
Momma rented the kitchen, table was all weight<br/>
Burnt spoons residue up In my cornflakes<br/>
Turn the TV on and find porn tapes<br/>
Who the fuck is sleeping in my hallway<br/>
Big John got the back yard like Broadway like all day<br/>
Epidemic for real<br/>
The shit is set up in the ghetto that the senate instilled for eugenics and bills<br/>
My whole family got the brunt of it<br/>
The effect on our genetic ill, smoke a blunt to it<br/>
40 glass broken on the ball court<br/>
Metaphor for why niggas always fall short<br/>
Crooked cops hospital with crooked docs<br/>
You dying they just look and watch<br/>
Shit's real no stamps gotta skip meals<br/>
Kids get killed depending how pigs feel<br/>
And to them it's not even a big deal<br/>
It's just another little black nigga from the hill<br/>
It's plenty more, I ain't taking it any more<br/>
My Chevy door gotta machete sword for the shredded pork<br/>
I blame it on the crack or the Betty Ford<br/>
12 steps just just to see it's far many more<br/>
Hello, my name's Cam I'm an addict<br/>
It's more like a lifestyle than a habit<br/>
I can't shake it can't beat I gotta have it<br/>
Positive attracts negative like a magnet

## Smoke & Mirrors 2: The Crack Baby (2015)

### 1) OhMaLawd Lyrics

[Intro: Cambatta]<br/>
Do what I do<br/>
I say what I say<br/>
Oh my lord, oh my lord<br/>
Oh my lord, oh my lord<br/>
Smoke<br/>
[Verse 1: Cambatta]<br/>
The government is evil<br/>
They're fuckin' with the people<br/>
And none of it is legal<br/>
And none of us believe you<br/>
Don't let a bubble-butt deceive you<br/>
Soon as your funds is up, she'll leave you<br/>
No matter what you trust, it's "fuck you"<br/>
If you bummy but if ya money's up they need you<br/>
Eeny, meeny, miny, moe<br/>
Kidnap your kid and don't let him go<br/>
Put a ransom on his head<br/>
If you don't get the bread, then he dead when that metal blow<br/>
Never commit to a ghetto ho<br/>
She only fuckin' to get the dough<br/>
Hole in your condom and now the ho pregnant<br/>
But is you the daddy? You'll never know<br/>
Left out of C-T, the weather cold<br/>
How I'm in Florida with heavy snow<br/>
Seven O's, pedico, Chevy door<br/>
Headin' home from med-i-co<br/>
There they go, there they go<br/>
Steady, slow; window down, let it blow<br/>
Check if they dead, and I roll<br/>
This is how everyday go<br/>
Most recite-able<br/>
Most reliable<br/>
Dope supplier who's quotes inspire you<br/>
Don't hold me liable<br/>
Hope you don't overdose and die<br/>
And you grow for higher<br/>
So don't deny the truth<br/>
You speakin' to the man<br/>
Speakin' to the man that wrote the Bible<br/>
Lord<br/>

### 2) God On Crack Lyrics

[Intro: Cambatta]<br/>
I'm just a fuckin' fiend in a long-ass dream<br/>
So fuck you, and everything in between<br/>
[Verse 1: Cambatta]<br/>
I'm sleepin' in the bed that they conceived me in<br/>
Checkin' in the hotel they shot King up in<br/>
The podium they shot X, while I preach to them<br/>
The opium that got Basquiat's what I'm cheefin' with<br/>
I'm fuckin' in that manjor they birthed Jesus in<br/>
Climax, leave it in<br/>
Never shall we meet again<br/>
I'm drinkin' out that cup that Christ bleedin' in<br/>
Cookin' crack in the pot that the rich man's peein' in<br/>
I'm cummin' in the womb that you came up out<br/>
I came up in before you even came about<br/>
My sperm saw the egg and had to change its route<br/>
Crack baby; I'm just lucky that I made it out<br/>
I take the crack up out the water and strain it out<br/>
Crack schemes make the crack fiends rave and shout<br/>
Swimmin' in an ocean full of slave bones<br/>
I'm a hostage of the giver of the bank loans<br/>
Every time I leave my porch, I shoulda stayed home<br/>
I get that liquor in my system and brake, bones<br/>
[Hook: Cambatta]<br/>
I promise you don't want it with the 'Batta man<br/>
I promise you don't want it with the 'Batta man<br/>
I never felt the embrace of my father's hand<br/>
That why that thang-thang is braced up in 'Batta's hand<br/>
All my life I get so high that I don't wanna land<br/>
What would you do if your God told you that his God is Cam'?

## Smoke & Mirrors ( The Porch ) 2013

### 1) Sounds of the Cosmos ( The Porch ) Lyrics

Monumentas occassion<br/>
Congregate on the porch the conversations engaging<br/>
Pot is blazing I'm waiting<br/>
Direct deposit at midnight<br/>
I'm got them hating<br/>
They ain't fucking with me I'm like ovulation<br/>
Contemplating on this Dali painting<br/>
My persistent memory is telling me that time is wasting<br/>
I only fuck with shrooms on occasion<br/>
And when I do I make observations<br/>
Connecting with the constellations<br/>
And now I have a different outlook on that plot in matrix<br/>
Eating fried chicken with the oracle<br/>
You would think cuz she was black that it was good .... it's horrible<br/>
Words of a wise man<br/>
Wings of a bird when I'm heard I do not land<br/>
What your hearing in your headset is not cam<br/>
It's a musical expression of who I am<br/>
Thats a scientific Explanation<br/>
Prophecizing Like a Mayan with a education<br/>
I drop rhyme and deep inside you feel in-trepidation<br/>
Cuz im tighter Vagina of a the freshest asain<br/>
Multi syllabical acrobactical<br/>
Rapping in algorhytms capatible to what apple do<br/>
Shaq Fu slap you til black and blue<br/>
That dudes bad new to these rapping crews<br/>
Im was Cultured in petree dish<br/>
I can't live im to focus We exist<br/>
I don't hate humans it's just Most of em are Devious<br/>
I feel a war coming I'm soldier I will bleed this<br/>
Im pleading the first listen and Plead the 5th<br/>
Columbian devils breath Breathe and sniff<br/>
My thinking shifts as the seasons switch<br/>
Aye royce Tell rhianna im a sink her ship !

### 2) Brief Conversation Lyrics

As I analyze life I question every facet<br/>
Like what it really takes to get that legendary status<br/>
Like do I have to dance around the stage like a tap dancing nigga or can I just talk with y'all<br/>
Like Professor X can't and walk wit yall<br/>
Cuz nobodies perfect there is fault in all<br/>
If you ever trip ill Support your fall<br/>
Cuz maybe your not ready for that walk let's crawl<br/>
Or better yet lay here stare up at the stars<br/>
And talk about those monuments appearing up on mars<br/>
Visuals of niburu and spiritual and rituals with ayawauasa witches brew<br/>
I'm Clearing all my thoughts<br/>
Apperently lost<br/>
But If parents were just parents all this fear in me that haunts<br/>
Won't infer wit me at all<br/>
My therapy is songs<br/>
And I know I That I can make you all adherent if it's strong<br/>
And lyric are da bomb<br/>
(Verse 2)<br/>
Tick tick boom<br/>
Gotta rich soon<br/>
The time on this wrist is<br/>
666 doom<br/>
Ita Hectic the right side of Slick Ricks room neglected<br/>
I hate it when I'm in this mood<br/>
Eye I patch my wounds with magical green flowers<br/>
Sex food and music im using that sweet sour<br/>
Pop a oxy like a moron<br/>
Wordplay<br/>
It's still Wednesday bitch why you Thursday

### 3) Jazzterbation Lyrics

My brain got a hard drive in it<br/>
3 terabytes of mc perasites<br/>
New Js saturdays coppin pair in site<br/>
Never will I wear em twice<br/>
I never had a fear of heights but my degree is of highest of the fareinheits<br/>
And my demeaner is the lowest of the Celsius and my got wallets potential is of the wealthiest<br/>
No lion I'm allergic to cat fur everything I say is a superflous rapture<br/>
Down periscope I submerge em in rap verse<br/>
Before we converse get a surgical mask first<br/>
Epidemic you can catch and spread it, but if your intellect less then you can never get, hepatitis free but my abc's are ill<br/>
Since I arrived every mc needs a will<br/>
Smith no wesson<br/>
Slick like the oil no need for the weapon<br/>
I follow with an answer if you lead with a question<br/>
I write it in stone cuz I down need a correction<br/>
Energys what I'm spreading<br/>
Like I'm bleeding ephedrine<br/>
Im the Leader of the league of the legends so i<br/>
Compete with aggression<br/>
To leave an impression<br/>
Cuz trying to suceeds an obsession<br/>
Im Sac religious<br/>
But black and gifted<br/>
Got glasses on but never lack the vision<br/>
Like a mathematician<br/>
Cash and sinning<br/>
Is a everyday thing like<br/>
Blacks in prison<br/>
I see thru it like the fabric linen<br/>
So im carrying protection like magics women should I ain't mad I'm winning tho im in debt paying lifes tolls for my bad decisions<br/>
So what do say<br/>
Am I the kind a artist you would go outta your way, to listen to<br/>
Or is there more I should be given you like better visuals or something more political more story line, gangstas criminals, or go the royce route and brag about genitals, couple chicks songs, something more spiritial, or skateboard shit like kick flips verials, well i am like RODney mullen I'm nice on the boards but im hardley stuntin I think just do me tho No regrets no sorry buttons

### 4) Lyrics Mckenna (Bring It On) Lyrics

Mental visions Of a young Terrence mckenna<br/>
I feel em when I'm rhyming<br/>
I'm chilling Vibin tripping psysiban singing phyllis hyman<br/>
Rhythm can splitta diamonds<br/>
I come across smart<br/>
Metaphorically I'm Noah lost ark<br/>
I'm 2x times you when a thought sparks<br/>
I don't just rap this is called art<br/>
Steady strumming on the strings of life<br/>
Heavy trumpets steady humming I can see light<br/>
Heavy drumming steady bumping<br/>
So I'm free to fight<br/>
For liberation of thought for you me alike<br/>
I orchestrate like a heterosexual whale<br/>
On the shores of great ness<br/>
Bare witness to arms that they bare wit surrender like bear victim<br/>
<br/>
to cash air sniff it Breathe<br/>
My olfactory bulb is money motivated<br/>
II'm stuck in a rut that our<br/>
Country cultivated<br/>
We product of ghettos people wit doe created<br/>
We can cry a river of blood and money will golden gate it<br/>
I'm jealeus of Jesus it seems he Jehovah s only favorite and why ain't he Savin the kids kony supposly slaying<br/>
My hope is tainted<br/>
Smoking haze and<br/>
Tryna give the beat the same heat hovi gave it<br/>
Flow Retarded like in<br/>
Pro creating when both related<br/>
You a fat boys plate overated<br/>
My body 25 but my soul ancient<br/>
Hoping my story got 50 mo pages<br/>
Working like a Cuban with a visa til I'm making purchases like mark Cuban with a visa<br/>
Moving like a cheetah<br/>
Think as monumental as the ruin up in giza<br/>
You the Brutus to my ceasar<br/>
Bread like pita<br/>
Do it for my dawgs like peta<br/>
Sick of handling a pan like peter<br/>
Heater ..... hand<br/>
The chemistry is magnetic<br/>
Turn your life to a memory in see half second<br/>
But that ain't me see my energy is in rap session and keeping pussy around me I call it aesthetics<br/>
Never jealous I'm just mad zealous chubby nigga with a wallet full of a mad lettuce<br/>
Raisen the level<br/>
Of the the bass and the treble<br/>
Turn my volume up to the max<br/>
Til it's shaking ya rental<br/>
Cuz me to musics like<br/>
Braces to dental it keep me straight when I stressful the monster within me will change in the jekel<br/>
Baggin sagging Barry mane<br/>
In a cadillac With a half a bag mary jane<br/>
Numbing life so I dont feel the pain<br/>
Since I went insane on shrooms shit I ain't been the same<br/>
More enlightened<br/>
Demigod I comquered strongest titan<br/>
Emancipated my state of mind I called<br/>
It zion<br/>
Daniel when he fought the lion I'm lying<br/>
I'm David slingshot to you giants

### 5) Spaceship Lyrics

[Verse 1]<br/>
I’m getting higher than a sky scraper<br/>
Last year i smoked five acres<br/>
1 blunt 5 flavors this is my nature<br/>
I get the whole world high with just my vapors<br/>
My Divine savior resides in this white paper<br/>
It's like a light saber I use to ignite haters<br/>
I say my prayers but to a different god<br/>
They found me in a capsule in an unidentified crater<br/>
Superman like Shaq from ‘99 Lakers<br/>
You’re like Vin Baker meets Von Wafer<br/>
Blahzay blah mamacusaa<br/>
Cambatta boombiyah hallelujah<br/>
Allah Akbar if heaven’s real then I'm not far<br/>
I keep a lot in that pot jar in my sock drawer<br/>
And I bet it be the freshest weed you ever seen<br/>
I'll call you out like Primrose Everdeen<br/>
I flow deep like the seven seas<br/>
With more joints than eleven knees<br/>
There's an alien inside of my flesh<br/>
E.T. phoned home tryna get to me<br/>
My blunt is like a spaceship<br/>
I’ma take you every where I take it<br/>
I take trips to other planets for strange shit<br/>
All I need is a studio and a blank disc<br/>

### 6) The Chronic Lyrics

[Verse 1: Cambatta]<br/>
They say I'm sitting on a high horse<br/>
It's cuz I'm clam baked in a mustang<br/>
I used to not smoke cuz my father did<br/>
I wasn't really fucking with the drug thang<br/>
But now I'm stressed out and I'm older<br/>
Got the weight of the world upon my shoulders<br/>
Got high the first time with my uncle Mark<br/>
Turned little Cambatta to a smoker<br/>
But I love him for that<br/>
I been destined for this since i started fucking withPpat<br/>
You would think we was blood brothers if I wasn't so black<br/>
So many times that I've been broke he'd slide a bug when he dap me like “here”<br/>
It’s a double edged sword<br/>
No matter how many blunts I always want more<br/>
I'm counting out pennies, I’m walking to the store<br/>
Fifty cent Phillies, I smoke my lungs raw<br/>
[Hook: Rafijah Siano]<br/>
[Verse 2: Cambatta]<br/>
Eddie deuce<br/>
Beat so gutter like belly juice fresh with the setups ooh<br/>
I get it cracking like Zeus when he let em loose<br/>
I need green can’t live without vegetables<br/>
I stay high when I’m in the booth<br/>
And fuck a job a neck tie means I'm in a noose<br/>
Analyzing my piss<br/>
The nurse opened up the cup and got high from the shit<br/>
Potent, Barsenio, A.R. semi go<br/>
Back to Africa where my soul can forever glow<br/>
Braid at the bottom of my Eddie fro let it grow<br/>
Marry that first ho that barks when I say to go<br/>
Whoa, that's the shit that I be thinking ‘bout<br/>
When I smoke I take life and pull the meaning out<br/>
When I cop it better even out<br/>
Or I’ma get it popping like a blunt that I forgot to pull the seeds up out

### 7) Anti Gravity Lyrics

Gravity defiant<br/>
Aiming for the Heavens til I'm actually in Zion<br/>
Rewriting the books in the Academy of Science<br/>
Invisible wings I imagine that I'm flying til I'm passing through Orion<br/>
Getting high like the Ribbon in the sky<br/>
I'm so fly I can tie it in a bow, whoa<br/>
Aerodynamic every time I flap my wings<br/>
Butterfly effect I'm remapping things<br/>
Aware of every change that my actions bring<br/>
I question everything I'm like Larry King but I rap and sing<br/>
I’m more open minded got blacker genes<br/>
I swear right hand on the Bible<br/>
But for my right hand man I’d lie on trial<br/>
My life on vinyl, the fact we don’t die kinda got me suicidal<br/>
Cuz what if my energies reabsorb in the cycle<br/>
And I come back as your idol with memories of my past life, I'll be mad nice<br/>
Battle of the white vs. black Christ<br/>
Or is it all a lie, zeitgeist?<br/>
I’m just tryna live life twice<br/>
I just gotta roll the right dice<br/>
Relying on the chronic til I'm dying like I'm sonic<br/>
When he's fighting with Robotnic<br/>
It's most likely hydroponic<br/>
I siphon all the knowledge til I’m righteous like Muhammad<br/>
I think about nature and all of its behaviors<br/>
And how it all relates to my purpose for the greater<br/>
I'm servicing my neighbors smoking purple til it’s vapors<br/>
Not the purple like the Lakers talking herbal I'm the bakers man<br/>
If you shake my hand<br/>
You'll taste weed residue if you taste your hand, I smoke<br/>
Money is the devil slavery is real<br/>
I'm working half my life away to pay these fuckin bills<br/>
I smoke a little weed just to brighten how I feel<br/>
Then they throw me in a cage with 30 days to appeal<br/>

### 8) Tronological Slaughter Lyrics

All hail to the late bloomers who should’ve made it way sooner<br/>
But put in work and now they spreading like a brain tumor<br/>
I’m pop locking in my grey Pumas<br/>
I hot box in front of state troopers<br/>
They call me Luther cuz I'm in the van with the dro like the gay crooner<br/>
Speaking of gay fuck J. Hoover, he's JFK' s shooter<br/>
I like gays I think Frank’s super<br/>
I really hope he has a great future<br/>
But what you do in your bedroom keep to yourself bruh I'm straight cooter<br/>
Booty and fake hooters! Who do it like they hoovers!<br/>
A couple of them Fifty Shades of Gray cougars<br/>
And show ‘em the dark shade is way cooler<br/>
Batta man leader of the Taliban<br/>
Taking over all the land you can call me Charlemagne<br/>
I'm raping ya with the Saudi for the oil<br/>
Assassinating you like Gaddafi cuz you’re loyal<br/>
It's all for the spoils of the royal<br/>
Meanwhile I'm getting roots deep in the soil<br/>
Seed sprouts, busting through concrete I'm free now<br/>
The rose that grows from street trials<br/>
In the physical realm I'm not free<br/>
But in the metaphysical realm God’s me<br/>
Inherited the words from Ali<br/>
So he don't gotta talk, his voice inside me<br/>
Platinum FUBU, my tapes aces first packs from Lulu<br/>
Stack is noodles sincere I'm tryna go back to Zulu<br/>
New jack I hate paying taxes screw you

### 9) Doctrine of Liberty Lyrics

I'm lost in a mental labyrinth<br/>
I’m a person with a purpose that accidentally happened<br/>
Hovering through life like Spike Lee camera angles<br/>
Society has noosed my neck it appears I'm strangled<br/>
Death so close I can hear the angels<br/>
Singing Pledge of Allegiance to the flag of a devil in a halo<br/>
Gave us paper for our gold<br/>
Ankle bracelets on our souls<br/>
They tainted mother nature and they raped her through her holes<br/>
Invisible jail cells<br/>
Digital augmented realities<br/>
Social security numbers are human barcodes<br/>
There’s an oil spill on aisle 666<br/>
This is a game of monopoly<br/>
That they play with economies<br/>
Psychological ball and chain<br/>
A 9 to 5 is a third of my life<br/>
After all the eating, fucking and sleeping all I have time to do is cry<br/>
If we all know were gonna die, why are we so content with not living ?

### 10) Lawdamercy Lyrics

[Verse 1]<br/>
I'm tight roping the Grand Canyon I'm high as fuck<br/>
My pipes holding a gram damn it I'm tryna puff<br/>
A psycho I'm the Van Damme of this rhyming stuff<br/>
It's my flow that advanced planets are tryna clutch<br/>
So throw your diamonds up, but where is your pride?<br/>
Know how many tribes and innocent lives in Africa died so you can be shining up?<br/>
But still you at jeweler buying stuff cuz when you shining hoes is lining up<br/>
See I don't bother with designers much, I can't afford to pay the price for lust<br/>
Light the Dutch, I'll be smoking til i bite the dust<br/>
High as heaven telling Christ what up<br/>
I be blessing every mic I touch, tiger punch!<br/>
Ken and Ryu, Guile Bison punk, genocide in every rhyme I bust<br/>
The state of Florida got my license fucked I rather stay at home then ride the bus<br/>
The greatest hustler ever I'm a mighty con<br/>
You my gayest customer ever, you a maricon<br/>
I write a song and ignite a bomb I’m a silent fire arm<br/>
Inside the palm of a child soldier reciting psalms<br/>
Amen<br/>
Lawdamercy<br/>
When I die just bury me In a Jordan jersey<br/>
[Verse 2]

### 11) Harry The Tubman Lyrics

[Verse 1]<br/>
Only some of us live but all of us die<br/>
None us laugh as much as we cry<br/>
All of that beauty with nothing inside<br/>
All of that money and none of your pride<br/>
None of you fight you run and you hide<br/>
But only the strong are gonna survive<br/>
The country is under corruption it's running on nothing but money were trusting their Lies<br/>
They puppet our lives<br/>
If I told you bout all of this stuff on my mind i can swear that my tongue'll be tied<br/>
Either that or in government custody stuck in them cuffs with a gun in my side<br/>
If my sisters and brothers combine<br/>
And we let all our love intertwine<br/>
Like the sun we gon shine cuz all us one of a kind<br/>
There’s nothing but time<br/>
But we waste it on chasing the paper<br/>
And banging on haters and hunching them dimes<br/>
All this shit is disrupting your grind<br/>
Only truth when it comes to the rhymes<br/>
Beautiful music is something divine<br/>
Visionary I’ll uncover your eyes<br/>
Flow is telescopic hubble with mine<br/>
Just come for the ride<br/>
[Hook]

### 12) Jazzterbation II (Left Hand) Lyrics

[Verse 1]<br/>
When I jazzterbate I bust<br/>
Beat jack you’re late, I’m on time<br/>
Mind over matter if the gold wasn't mined in my mind it don’t matter<br/>
But I still listen<br/>
Wipe the blood off of the diamond it still glisten<br/>
But the pain is still in them<br/>
Kids starving at the bottom of the food chain<br/>
I'm only one step up still tryna get a new chain<br/>
Back stroking through the ocean of hope<br/>
My body is haunted my soul is a ghost<br/>
That man in the mirror is only a host<br/>
The God in me is awoke when my vocals evoke<br/>
I serve scriptures, Caron Butler<br/>
Take a second let your mind buffer<br/>
To backboards I'm the top toucher<br/>
If Jay Z’s the goat then I’m Rucker<br/>
Niggas dying for attention<br/>
To point that they dying from the tension<br/>
Provider of your lessons, I’ll guide you while you rise into ascension<br/>
Divine as interventions of them Fivers in correctional facilities<br/>
Making brothers outta they enemies<br/>
Will I forever be a slave of my identity?<br/>
Or will I live like I can't die cuz I'm energy?<br/>
Fuck luck this destiny

### 13) Zeitgeist Haze Lyrics

Exhale vapors, gaze in the smoke<br/>
It's a ghost from the fire that I blaze when I tote<br/>
Celestial particles of my burn victims<br/>
Only sacrificing the herbs to earn wisdom<br/>
Rap scholar I’m down to my last dollar<br/>
Mad drama last saga of Andromeda’s me<br/>
What you’re getting is Cam’s heart on a beat<br/>
If struggle is quick sand then Cambatta is deep<br/>
Look I’ve seen a lot in my life, the trauma the strife<br/>
I'm locked in economy’s vice<br/>
Media’s molding our minds it's pottery night<br/>
Open your eyes, 9/11 was an obvious heist, truth<br/>
They’re taking our freedom, Obama is white<br/>
Religion’s just a depiction of the stars in the night, Chuuch<br/>
If knowledge is power and honor is might<br/>
Then life is a battle not all of us fight<br/>
I'm swinging, shadow boxing, my doctrines are like a jab I'm knocking facts into your noggin<br/>
You dodge em I'm Tim Bradley robbing<br/>
Snatch a nigga’s cash up off him slash him like a fraction problem<br/>
If my Dad’s watching I'm thankful that he ain't grab a condom<br/>
Original man with a cynical plan<br/>
To be a god and hold the world in the midst of hand<br/>
I'm taking my chromosomes and I'm switching the strands<br/>
Til I’m stronger than Arnold and smarter than kids in Japan<br/>
I'm tweeking, I spark chaos I'm part Aesop’s<br/>
I’m part Madoff and part Adolf<br/>
I parlay off shore in Barbados<br/>
With the rich white banking cartels that play golf<br/>
I’m sicker than a plague cough<br/>
Quicker then when dipping in a whip and it got straight naus’<br/>
Sipping liqour by the pitcher like it’s May 4th<br/>
Or is it may 5th, and I’m a straight spic?<br/>
Words are forms of expression I like to play with<br/>
By twisting them in complex rhyme patterns to make chips<br/>
Shit, I Got the grade a piff<br/>
And a Bajan bitch badder than Bebe’s kids<br/>
I’m James Naismith<br/>
I'm heated like Bayless vs. Steve A Smith, believe that shit<br/>
It's Batta I’m out of this world I'm like a spaceman<br/>
Since that keg stand with Mike’s water in Space Jam<br/>
Placebo effecting yall niggas<br/>
I don't even need substance to get to yall niggas<br/>
I'll shoot a 3 then steal it and shoot a 3 again<br/>
In 8.9 seconds and Reggie yall niggas<br/>
Ahead of yall niggas you ain't ready my niggas<br/>
If life was money blacks are pennies my nigga<br/>
You throw ‘em in the gutter, seclude ‘em from the lighter coins<br/>
Throw ‘em to a bum he spend it on crack and invite his boys<br/>
Your music is classified as a type of noise<br/>
My music clever like Trojan horses inside of Troy<br/>
They classify it as a new school sound<br/>
How my voice can project like Coo Coo Cal<br/>
40 acres a mule and a few thou<br/>
I'm Standing at my mailbox waiting it's due now<br/>
Smoke and mirrors life is like a magic show<br/>
A bunch of illusions for manipulating the average soul<br/>
But I can see that slight of hand<br/>
Looking close and digging deep’s how you defeat that kind of plan<br/>
Self sustain get knowledge and be happy<br/>
Smoke and mirrors coming soon, scream at me

### 14) The Watchmen Lyrics

[Verse 1: Cambatta]<br/>
Another posse cut<br/>
I'm the cocky fuck<br/>
That no one knows that fucked, the roster up<br/>
Then you spark a blunt &<br/>
hear a God amongst<br/>
Men-nonite (Men or Knight)<br/>
, Christ on cross with a pen to write<br/>
My ink blood, I'm penning life ‘til I’m heaven’s height<br/>
Do CID<br/>
,<br/>
And dream a dream so lucid<br/>
I'll travel back in time before you lived<br/>
Threaten your father a day before shooting you in<br/>
And make him fuck your mom to my music, like ‘Batta’s that new shit<br/>
I’m opposite Newton, I’m Scottie on Ewing<br/>
My shottie so spoiled, B-B-BRAT! I'm shooting<br/>
Fornicate a lot, I’ll record a rape and watch<br/>
While freebasing a quarter eight of rock, I'm stupid<br/>
Recognize patterns mind, Seven times Saturn wide<br/>
1/1 suicides, genocide, recognize<br/>
I forever shine so bright, that I’m wrecking eyes<br/>
Your retina’s blind like Helen's eyes<br/>
(Smoke!)<br/>
I'm sitting on the porch with my sociopathic ass<br/>
Liquor by the quart, and a O of that Cali grass<br/>
This shit is like a fort, I'm a soldier that battles tracks<br/>
Not a sacrificial lamb of that battle in Iran<br/>
I ain't chattel, I am cam<br/>
The lower case version<br/>
Still smoking dro, even though I ain't working<br/>
Fuck a vote ballot, I’m stuck in my home rapping<br/>
‘Till the flow is so dope I give Oprah a coke habit

## Visionary 2 (2010)

### 1) Stoopid Lyrics

[Verse: Cambatta]<br/>
I'm so guerrilla like Don Cheadle's face<br/>
I'm Earl Manigault before he needed base<br/>
I own stock in several separate Norwegian banks<br/>
Money transcends skin color, I don't need a race<br/>
My design was derived from Stan Lee<br/>
Unequivocal mind I combine with hand speed<br/>
Make a nigga look like he died by stampede<br/>
Even with a pair of God's eyes, you can't see<br/>
Me mother fucker, I'm critically acclaimed for dicking dames<br/>
And having chicks limping with a cane<br/>
Your reign on the top was short like Verne Troyer<br/>
Short like Allen I., before he turned Hoya<br/>
My vocal abilities paranormal activity<br/>
You don't see me visually, but you hear, and you feeling me<br/>
So like it like a simile, or hate it like a enemy<br/>
I got a big face, for every leg on a millipede<br/>
[Hook:]<br/>
[Verse 2: Cambatta]<br/>
Out of this world shit E.T.'s diaper<br/>
I prove it in the next B.E.T. cypher<br/>
Enough bail money to release three lifers<br/>
And I ain't lying/lion, I'm a liger<br/>
Every time I lay a hook, I'm feeling like I'm Beowulf<br/>
Fucking chicks good enough to make them want to stay and cook<br/>
Better not be hot grits, I be on that rock shit<br/>
Rougher than a mosh-pit, disgusting like some hok spit<br/>
Hypothetically speaking, if I have never been beaten<br/>
And my genetics are reaching a levels medically beasting<br/>
Colder than the weather when the temperature's freezing<br/>
So that word hypothetical is technically treason<br/>
I'm a rottweiler mixed with a swamp monster<br/>
Mix that with John Conner, shitting on you dot com'mers<br/>
I got them sweating like a hot sauna<br/>
It's bata-bata, the top dollar<br/>
Black guido I pop collars

### 2) So Good Lyrics

[Sample]: br/

It's so good<br/>
It's so good<br/>
(Reasonable)<br/>
It's so good<br/>
[Verse One] [Nino Bless]:<br/>
Nino!<br/>
Ayo, it's so good how I do this<br/>
Your flow is Sarah Palin stupid which don't pertain to my music<br/>
Content, I constantly rock shit,<br/>
I rhyme sick<br/>
You just rhyme sick like stick, slick<br/>
Simple one syllable ass rapping shit for brains<br/>
I'm like the new Big Daddy Kane minus the pimping thang<br/>
A young Rakim minus the sniffing cane<br/>
A young G. Rap on these Roads To Riches switching lanes<br/>
The kids insane, raising the stakes soon<br/>
I blaze tunes to make the elephant change rooms<br/>
And I can't wait till I drop<br/>
Watch rappers get shook like Mickey Factz in a room with Rae's goons<br/>
Ice Water, mic's I slaughter<br/>
You will never see me in no one's shadow like Night Crawler<br/>
I'm 5'4" with an Eiffel height aura<br/>
Sneaking into your top five now put it in size order<br/>
You hearing Nino's flow on tracks and (it's so good)<br/>
Damn, huh<br/>
These cats is all hype but ain't killing the mic feel me (yeah)<br/>
Yo Crook we going innnnn
