<p align="center"><img width=50% src="https://raw.githubusercontent.com/DataCloud-project/toolbox/master/docs/img/datacloud_logo.png"></p>&nbsp;

[![GitHub Issues](https://img.shields.io/github/issues/DataCloud-project/R-MARKET_SMS.svg)](https://github.com/DataCloud-project/R-MARKET_SMS/issues)
[![License](https://img.shields.io/badge/license-Apache2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# R-MARKET SMS

What is it?

* The R-MARKET Secret Managment Service (SMS) developed based on the iExec-sms. It stores secrets which are then usable in the iExec network.
* This key component makes possible for anyone to compute confidential assets on the iExec network.
* This component is mandatory to enable the TEE (Trusted Execution Environment) mode of the iExec network.
* The R-MARKET SMS provisions secrets to remote applications that are running inside identified & trusted enclaves.
* Confidential assets you have (e.g., password, token, API key, AES key, etc.) should be securely transferred from your machine to the SMS over a TLS channel (iExec SDK is recommended). This operation is only done once.
* Internally, secrets are encrypted with standard AES encryption before being written to disk. 
* The R-MARKET SMS secret provisioning policy is based on on-chain ACL (PoCo). PoCo smart contracts define simple ACL rules where individuals have ownership of on-chain objects they have deployed (workerpool, application, secret-dataset & requester).
* Each individual who is the owner of an object could define a policy on it. For example, "As a Requester (0xAlice), I only authorize my confidential Secret-Dataset (0xSecretOfAlice) to be used by the application of Bob (0xAppOfBob) I trust which will run on the Workerpool of Carl (0xWorkerpoolOfCarl)".
* When the secure application of Bob starts, the secret of Alice is written into a temporary session and sent over TLS to a dedicated  Configuration & Attestation Service (CAS) enclave responsible for communicating with the final application enclave.
* If the application enclave is legit (measurable with its mrenclave with Scone), it will receive the secrets.
* To sum up, if all checks are correct, the secret of Alice will cross the following environments: Alice-Host -> iExec-SMS -> Scone-CAS -> Bob-Scone-Application
