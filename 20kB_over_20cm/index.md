# 20 kB over 20 cm

I can send a gigabyte to the other side of the planet with relative ease, in most situations. If I have a 40Mbps down connection in some random café or on my phone I can download 1GB of data in 3 minutes and 20 seconds. At home or at work i have significantly faster speeds than this. It is incredible that we can send that much data from almost anywhere to almost anywhere. But what if I want to send 20kB to something just 20cm (~8 inches) away? How would you do this?

My first instinct is to send a file over signal (the end-to-end encrypted chat). This requires that both endpoints have signal, they have to have each other as contacts, they have to be connected to the internet and be able to connect to signal's servers. My phone, laptops and desktops fulfill these requirements almost always. But this is sending the traffic very far (to signal's servers) before it goes back to 20 centimeters away. I've used this to share URLs between devices, or send small scripts between machines.

A more common approach (I imaging) would be email, which has the same problems plus it's not E2EE. More people have email however, so this technique works more often. I've used this approach to send a list of names between two computers, where only one of them was mine.

When sending files to computer nerds who are on the same local network as me, I've used netcat to send files.
```bash
# Computer receiving the data
$ nc -lvp 1337 > received_data

# Computer sending data
$ nc 192.168.0.54 1337 < data_to_send
# you have to press ^C to quit the transfer on either end. Netcat doesn't do that by itself.
```
This requires being on the same network, knowing the recipient's ip address, both having netcat and probably bash (or some other shell that supports redirecting output to a file). You also need to both be massive nerds. This works well with hackers. It's not encrypted, but the traffic also doesn't go very far. Privacy wise I would say this is better than email. Usually the data isn't stored in some third computer (like the cloud) either, which is nice. It

If only one of you is a huge nerd, you can try this.
```bash
$ mkdir files_to_share
$ cd files_to_share
$ mv ../data_to_send .
$ python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
# Make the other computer go to http://<ip>:8000/
```
This requires that the sender has python installed and the receiver has a web browser. AFAIK Windows doesn't have python by default but macOS does and most Linux machines do as well. Depending on your local network speed this can actually be the fastest way to send any amount of data. I've sent movies (>1GB) like this. This doesn't work very well to send data from a phone.

All of these have been over IP on some level, and only involved devices that have very advanced execution environments. Phones, laptops and desktops can all run web browsers. Bluetooth runs on significantly smaller devices than that, like my flipper zero. Or a PineTime ("open" source smartwatch[^open]).

Things that allegedly would solve this:
- Airdrop (I only have 1 apple device)
- Bluetooth (I remember sending small mp3s over bluetooth when I was 10. Why does no one use this feature anymore?)
- USB drives (I rarely have these on me anymore. They suffer from data being hard to remove from them.)
  - One of my friends had this USB drive that had both USB-A and USB-C, which was very neat. Maybe that would be good for phones (except iPhones with lightning cables)
- (micro)SD cards (same as above)

I can't really evaluate these as I don't fully understand them. But I haven't had success with any of these. I started thinking about the small data over small distance problem after spending over an hour trying to send some key data from one flipper zero to another. It was like 100 bytes or something. If we had a hex editor on each flipper it would've been faster to type them by hand. It would be nice if there was a very commonly implemented way to do this. I'd like to hear how you do send small files small distances! You can post about it [here](https://queer.party/@polly/112631214527004578)

[^open]: It's not open hardware, they don't give you the schematics or boardview files. There's even weird restrictions on some of the peripherals' firmware. So it's only kinda open. Which is why they write open source and not open hardware, I suppose. It depends on if you think the source in open source refers to only source code or like everything they give you.
