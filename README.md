# SOC---Email-Analysis

## Introcuction

In this project I as SOC Analyst delve into the critical topic of email analysis specifically phishing.

![Screenshot 2024-04-23 130209](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/a7a5e12a-3345-477b-bf85-620abecdedf4)

By analysing this email I see some suspicious indicators:
- spf=failed (google.com: domain of billjobs@microappl.com does not designate 93.99.104.210 as permitted sender) - in other words microappl.com does not who is 93.99.104.210, good indicator of suspicious email, if spf is set to fail it good sigt to take a dip look into it.
- I see 'From: "Bill" billjobs@microapple.com and 'Reply-To: 'negaja3921@pashter.com', because of discrepancy betweenthe two, that is pretty suspicious
- Then i see 'Content-Type': multipart/mixed; boundary=BOUND_600FB98E0DCEE8.49207210' which means how to render the content of email with it bein multipart/mixed (means has multiple formats), and also boundry set for it 'BOND_600', means when to start and stopredndering the content usin the certain format.

Now let's see the content of the coded text, decode it with base64

![Screenshot 2024-04-23 133555](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/39f008a1-b2ab-4014-be37-e7b3dda55f6d)

After decoding the output is:

![Screenshot 2024-04-23 134028](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/4b3afd34-309d-4257-8bb9-20beb95cd6d3)

Now investigate the next part of the email with pdf file, copy content and decode it using base64:

![Screenshot 2024-04-23 135820](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/28a13518-8ce3-4830-86b2-835a1c0a5f0f)

And as i can see base64 doesn't work with this content, let's find out what is the format of this file, so convirt content into hexadecimal format for find out the signature of the file:

![Screenshot 2024-04-23 140103](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/3e757f50-d156-4e6e-9d5a-9c2db9d40607)

As i can see from first few bites '50 4b 03 04' i found something interesting in here - ZIP extension. Instead of 'pdf' its ZIP now:

![Screenshot 2024-04-23 140505](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/b61f2c14-e779-42a1-95bd-320a5db7e0f1)

After extracting files i see three files, including of one hidden file with xlsx extension, let's investigates the files:
- utilazing HxD I difine the first file and founf out the format of that - jpeg 
![Screenshot 2024-04-23 142336](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/12b9cca6-a57e-4a9f-8e4d-b38d2a940d4c)
![Screenshot 2024-04-23 143302](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/c396329d-ac2f-461d-88a3-55df4c6064ca)

The same process for second file - pdf.

Now let's check if provided xlsx file is really xlsx.

![Screenshot 2024-04-23 143914](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/31615ba9-43f1-4ef2-8cb9-8b0da0d21a69)

As I can see that is real xlsx file. Not using SquareX app checking safely opening the file.
Nothing suspicious inside, expept hidden text on the 'Sheet3', found hidden text after clear format:
![Screenshot 2024-04-23 145146](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/912597ee-c40e-4c6d-bb39-2ab68d2ba8e3)
![Screenshot 2024-04-23 145209](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/57f632fe-3bd3-4e1a-ac30-12f2adc6c885)
And the last one is decode the message:
![Screenshot 2024-04-23 145301](https://github.com/AndrewTanga/SOC---Email-Analysis/assets/93886645/dd3921f1-869f-4d6d-95c7-5ba7e87303a9)










