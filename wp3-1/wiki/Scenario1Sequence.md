Scenario1 Sequence Diagram[¶](#Scenario1-Sequence-Diagram)
==========================================================

<div class="uml">title Scenario 1\nGeorge wants to view his mobile hosted MP4s on his set-top-box\nand both devices have access to the internet

actor George
participant "George's mobile" as George_mobile
participant "George's set-top-box" as George_set_top_box

autonumber

== identification ==

group identification example
	George -> George_mobile : switch on
	George_mobile -> George : ask the pin
	George -> George_mobile : provide the pin
end

== device discovery ==

group device discovery example
	note over George, George_mobile : the user may set a policy to automatically\nstart device discovery
	George --> George_mobile : <font color="gray"><i>start device discovery</i></font>
	George_mobile -> George_set_top_box : broadcast hello message
	George_set_top_box -> George_mobile: hello response
end

== personal local cloud join ==

note over George, George_mobile : the user may set a policy to automatically\nselect devices to autenticate and join.\nthree possible solutions are:\n- try to authenticate every sensed device\n- maintain a local membership list\n- maintain a remote membership list
George_mobile --> George : <font color="gray">show available clouds and devices</font>
George --> George_mobile : <font color="gray">select the set-top-box</font>
George_mobile -> George_set_top_box : George's mobile authentication
George_set_top_box -> George_mobile : George's set-top-box authentication

note over George_mobile, George_set_top_box : personal cloud devices can use their shared secret to\ndistribute session keys and establish secure channels
George_mobile -> George_set_top_box : establish a secure channel

== service provision ==

George -> George_mobile : ask for MP4 list
George_mobile -> George_set_top_box : MP4 list retrieval
George_set_top_box -> George_mobile : MP4 list transmission
George_mobile -> George : MP4 list display
George -> George_mobile : MP4 selection
George_mobile -> George_set_top_box : MP4 retrieval
George_set_top_box -> George_mobile : MP4 transmission
George_mobile -> George : MP4 consumption</div>

-- "Personal local cloud join" open points --

How to select devices to authenticate?

a\) trying to authenticate every sensed device\
 Can a device enter in hidden mode?\
 Can a device access to an internet access points when it is in hidden
mode?\
 How can the device avoid to contact fake internet access points?
(locally maintaining a list of known access points?)

b\) maintaining a personal cloud membership list in a local always-on
membership manager device (MMD)\
 b.1. George's mobile authenticates the MMD\
 b.2. George's mobile gets the personal cloud membership list from the
MMD\
 b.3. George's mobile tries to authenticate devices of the personal
cloud membership list

    How to maintain the list? physically accessing the master device? remotely accessing the master device?

c\) maintaining a personal cloud membership remote list (e.g. on WAP)\
 c.1. George's mobile connects to internet\
 c.2. George's mobile queries the DNS system to obtain the Membership
Remote Manager (MRM) address\
 c.3. George's mobile contacts the MRM\
 c.4. George's mobile and MRM mutually authenticate themselves\
 c.5. George's mobile gets the personal cloud membership list from the
MRM\
 c.6. George's mobile tries to authenticate devices of the personal
cloud membership list

    Assumptions in step c.4.    - George's mobile can trust certificates which are pre-installed into the device by the manufacturer, by the distributor or by the dealer.        - these can include the MRM certificate or the root certificate of the PKI who signed the MRM certificate    - if the MRM is in the WAP it can rely on the same user authentication used to issue the WeST    - if the MRM is not in the WAP it can accept the WeST for authentication

    Devices may have a local copy of the list to use when they are not on line.    How to maintain the list? After the authentication with MRM it should be possible to edit the list (used device can be member of the personal cloud or an external device)

-- STEP 11 remarks --\
How to establish the secure channel?

Personal cloud devices can use their shared secret to distribute session
keys and establish secure channels.\
They can use a pairwise session key for every channel and a common
session key (personal-cloud-wise session key?) for broadcast
communications.\
When a device leave the cloud may be necessary to renew the broadcast
key.

Diffie-Hellman Key Agreement can be used to set-up the secure channel.
Since there is the pre-shared key among all the devices of one user's
personal cloud, they also can authenticate another by using this key
during the D-H key agreement.

