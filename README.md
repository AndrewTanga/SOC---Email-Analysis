# SOC---Email-Analysis

## Introcuction

In this project I as SOC Analyst delve into the critical topic of email analysis specifically phishing.

![Screenshot 2024-04-23 130209](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/a7a5e12a-3345-477b-bf85-620abecdedf4)

By analysing this email I see some suspicious indicators:
- spf=failed (google.com: domain of billjob@microappl.com does not designate 93.99.104.210 as permitted sender) - in other words microappl.com does not who is 93.99.104.210, good indicator of suspicious email, if spf is set to fail it good sigt to take a dip look into it.
- I see 'From: "Bill" billjobs@microapple.com' and 'Reply-To: negaja3921@pashter.com', because of discrepancy betweenthe two, that is pretty suspicious
- Then i see 'Content-Type': multipart/mixed; boundary=BOUND_600FB98E0DCEE8.49207210' which means how to render the content of email with it bein multipart/mixed (means has multiple formats), and also boundry set for it 'BOND_600', means when to start and stopredndering the content usin the certain format.
