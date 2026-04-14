# What's Tag91

#### Definition and Purpose:

* Tag 91 in the context of EMV (Europay, MasterCard, and Visa) standards refers to 'Issuer Authentication Data'.
* This data is crucial for the authentication process during an EMV transaction. It is provided by the card issuer and plays a significant role in securing the transaction.

#### Operational Context:

* Host Response: Tag 91 is typically returned by the host (e.g., bank or card issuer's server) as part of the transaction response.
* Integration with EMV Kernel: Once received, the issuer authentication data in Tag 91 must be correctly set or inputted into the EMV kernel of the smart POS system. This step is essential for the completion and validation of the transaction process.

#### Key Considerations:

* Security and Compliance: The handling of Tag 91 data must adhere to EMV security standards and protocols to ensure the integrity and security of the transaction.
* Software Integration: Smart POS systems must have robust software capable of accurately processing and integrating Tag 91 data into the transaction flow.

#### Technical Implementation:

* Data Format and Content: The issuer authentication data may contain cryptographic information essential for validating the transaction. The format should be compatible with the EMV kernel's requirements.
* Error Handling: The smart POS system should be equipped to handle any errors or discrepancies in Tag 91 data, alerting the operator and taking appropriate actions as per defined protocols.

#### Usage in Transaction Process:

* During an EMV transaction, the smart POS system retrieves Tag 91 data from the transaction response and utilizes it as part of the issuer authentication procedure.

Note:

* Understanding and correctly implementing the handling of Tag 91 is vital for developers and technicians working with EMV systems in smart POS terminals. It ensures not only the security of transactions but also compliance with global EMV standards.
