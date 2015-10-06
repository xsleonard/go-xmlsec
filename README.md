# go-xmlsec

A (partial) wrapper for [xmlsec](https://www.aleksey.com/xmlsec).

## Signing Example

    key := []byte(`-----BEGIN PRIVATE KEY-----
    MIICeAIBADANBgkqhkiG9w0BAQEFAASCAmIwggJeAgEAAoGBAOK9uFHs/nXrH9Lc
    GorG6lB7Qs42iWK6mIE56wI7dIdsOuXf6r0ht+d+YTTis24xw+wjEHXrVN0Okh6w
    sKftzxo8chIo60+UB5NlKdvxAC7tpGNmrf49us/m5bdNx8IY+0pPK0c6B786Uluj
    Tvx1WFdDXh3UQPBclbWtFe5S3gLxAgMBAAECgYAPj9ngtZVZXoPWowinUbOvRmZ1
    ZMTVI91nsSPyCUacLM92C4I+7NuEZeYiDRUnkP7TbCyrCzXN3jwlIxdczzORhlXB
    Bgg9Sw2fkV61CnDEMgw+aEeD5A0GDA6eTwkrawiOMs8vupjsi2/stPsa+bmpI6Rn
    fdEKBdyDP6iQQhAxiQJBAPNtM7IMvRzlZBXoDaTTpP9rN2FR0ZcX0LT5aRZJ81qi
    +ZOBFeHUb6MyWvzZKfPinj9JO3s/9e3JbMXemRWBmvcCQQDuc+NfAeW200QyjoC3
    Ed3jueLMrY1Q3zTcSUhRPw/0pIKgRGZJerro8N6QY2JziV2mxK855gKTwwBigMHL
    2S9XAkEAwuBfjGDqXOG/uFHn6laNNvWshjqsIdus99Tbrj5RlfP2/YFP9VTOcsXz
    VYy9K0P3EA8ekVLpHQ4uCFJmF3OEjQJBAMvwO69/HOufhv1CWZ25XzAsRGhPqsRX
    Eouw9XPfXpMavEm8FkuT9xXRJFkTVxl/i6RdJYx8Rwn/Rm34t0bUKqMCQQCrAtKC
    Un0PLcemAzPi8ADJlbMDG/IDXNbSej0Y4tw9Cdho1Q38XLZJi0RNdNvQJD1fWu3x
    9+QU/vJr7lMLzdoy
    -----END PRIVATE KEY-----`)
    
    docStr := `<?xml version="1.0" encoding="UTF-8"?>
    <!--
    XML Security Library example: Simple signature template file for sign1 example.
    -->
    <Envelope xmlns="urn:envelope">
      <Data>
        Hello, World!
      </Data>
      <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
        <SignedInfo>
          <CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" />
          <SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
          <Reference URI="">
            <Transforms>
              <Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            </Transforms>
            <DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
            <DigestValue></DigestValue>
          </Reference>
        </SignedInfo>
        <SignatureValue/>
        <KeyInfo>
        <KeyName/>
        </KeyInfo>
      </Signature>
    </Envelope>`

    signedDoc, err := xmldsig.Sign(key, doc)
    os.Stdout.Write(signedDoc)
