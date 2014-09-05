Scenario 3 Sequence Diagram[¶](#Scenario-3-Sequence-Diagram)
============================================================

![ title : Scenario 3\\nGeorge wants to listen to Paul's MP4s on his
mobile\\nmobile to mobile, and both have access to the internet actor
George participant "George's mobile" as George\_mobile participant
"Paul's mobile" as Paul\_mobile actor Paul autonumber == identification
== group identification example George -\> George\_mobile : switch on
George\_mobile -\> George : ask the pin George -\> George\_mobile :
provide the pin end == device discovery == group device discovery
example note over George, George\_mobile : the user may set a policy to
automatically\\nstart device discovery George --\> George\_mobile :
\<font color="gray"\>\<i\>start device discovery\</i\>\</font\>
George\_mobile -\> Paul\_mobile : broadcast hello message note over
Paul\_mobile, Paul : For privacy reasons Paul MAY explicitly\\nturn on
visibility of his mobile for the\\ndiscovery process Paul\_mobile -\>
George\_mobile: hello response end == personal local cloud join ==
George\_mobile -\> George : show available clouds\\nand devices
George -\> George\_mobile : select Paul's mobile George\_mobile -\>
Paul\_mobile : George's mobile tries to authenticate note over
George\_mobile, Paul\_mobile : authentication fails because George's
mobile\\ndoesn't know Paul's personal cloud secret Paul\_mobile -\>
George\_mobile : authentication failed George\_mobile -\> Paul\_mobile:
ask for join permission Paul\_mobile -\> Paul : ask for join permission
Paul -\> Paul\_mobile: grant join permission group session key exchange
example Paul\_mobile -\> Paul : generate a session key note over
George\_mobile, Paul\_mobile : How to communicate the session key?\\n-
out-of-band\\n- by a clear, local channel (e.g. by bluetooth)\\n- by an
encrypted channel created without a trusted third party\\n (e.g. a
device can send his public key to the other one)\\n- by an encrypted
channel created relying on a trusted third party (e.g. WAP) Paul -\>
George : communicate the session key out-of-band George -\>
George\_mobile : insert session key end note over George\_mobile,
Paul\_mobile : devices can use the session key\\nto establish a secure
channel George\_mobile -\> Paul\_mobile : establish a secure channel ==
service provision == George -\> George\_mobile : ask for MP4 list
George\_mobile -\> Paul\_mobile : MP4 list retrival Paul\_mobile -\>
Paul : ask for MP4 list\\nsharing permission note over Paul,
Paul\_mobile : the permission is temporary because the\\napp user is a
personal local cloud guest Paul -\> Paul\_mobile : grant temporary
permission Paul\_mobile -\> George\_mobile : MP4 list transmission
George\_mobile -\> George : MP4 list display George -\> George\_mobile :
MP4 selection George\_mobile -\> Paul\_mobile : MP4 retrieval
Paul\_mobile -\> Paul : ask for MP4 sharing permission note over Paul,
Paul\_mobile : the permission is temporary because the\\napp user is a
personal local cloud guest Paul -\> Paul\_mobile : grant temporary
permission Paul\_mobile -\> George\_mobile : MP4 transmission
George\_mobile -\> George : MP4 consumption George -\> George\_mobile :
select another MP4 George\_mobile -\> Paul\_mobile : MP4 retrieval
Paul\_mobile -\> George\_mobile : MP4 transmission George\_mobile -\>
George : MP4 consumption
](http://dev.webinos.org/redmine/wiki_external_filter/filter?index=0&macro=plantuml&name=5b9ebc2b0308cdf969ddfdee57e322fafe7243201d3c1b74c498ac14e7698807)

-- STEP 15 DETAILS --\
How to communicate the session key?

a\) out of band\
 a.1. Paul reads the session key form his device\
 a.2. Paul tells the session key to George\
 a.3. George insert the session key in his device

b\) by a clear, local channel\
 b.1. Paul's device establish a local connection to George's device
(e.g. by bluetooth)\
 b.2. Paul's device sends the session key to George's device\
 b.3. George's device sends and acknowledge to Paul's device\
 b.4. Paul's device closes the connection

c\) by an encrypted channel created without a trusted third party (e.g. a
device can send his public key to the other)\
 c.1. Paul's device establish a local connection to George's device
(e.g. by bluetooth)\
 c.2. George's device sends his public key to Paul's device\
 c.2. Paul's device encrypt the session key using George's public key\
 c.3. Paul's device sends the encrypted session key to George's device\
 c.4. George's device decrypt the session key\
 c.5. George's device sends and acknowledge to Paul's device\
 c.6. Paul's device closes the connection

d\) by an encrypted channel created relying on a trusted third party
(TTP) (e.g. WAP)\
 d.1. Paul's device establish a secure channel with the TTP (using the
TTP public key)\
 d.2. Paul's device communicates to TTP the will to securely connect
with George's device\
 d.3. George's device establish a secure channel with the TTP (using the
TTP public key)\
 d.4. George's device communicates to TTP the will to securely connect
with Paul's device\
 d.5. TTP generates a secret key SK and communicates it to both devices\
 d.6. Paul's device close the TTP connection\
 d.7. George's device close the TTP connection\
 d.8. Paul's device and George's device establish a secure channel using
SK\
 d.9. Paul's device sends to George's device the session key\
 d.10. George's device sends and acknowledge to Paul's device\
 d.11. Paul's device closes the connection

    Assumptions    - the TTP can give his certificate to devices, which verify it relying on a PKI    - alternatively, devices can trust the TTP certificate inserted by the manufacturer, by the distributor or by the dealer

-- STEP 17 DETAILS --\
How to establish the secure channel?

George's mobile and Paul's mobile can establish a secure channel using
the session key.

