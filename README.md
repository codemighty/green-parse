Green PaRsE
===

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Pure-JS Green Pass Reader - EU Digital COVID Certificates (EUDCC) Reader

Porting from [vacdec](https://github.com/hannob/vacdec) by hannob.

Information about generated JSON: [covid-certificate_json_specification_en.pdf]( https://ec.europa.eu/health/sites/default/files/ehealth/docs/covid-certificate_json_specification_en.pdf)

Dati di test: [Link](https://github.com/eu-digital-green-certificates/dgc-testdata/tree/main/IT) 

## Demo

[certverde.it](https://certverde.it)

## The Code
Full and commented version on green-parse.js

```
const cbor = require('cbor')
const base45 = require('base45')
const pako = require('pako')

// Example qr code from https://github.com/eu-digital-green-certificates/dgc-testdata/tree/main/IT
const exampleQR = "HC1:6BFOXN%TS3DH0YOJ58S S-W5HDC *M0II5XHC9B5G2+$N IOP-IA%NFQGRJPC%OQHIZC4.OI1RM8ZA.A5:S9MKN4NN3F85QNCY0O%0VZ001HOC9JU0D0HT0HB2PL/IB*09B9LW4T*8+DCMH0LDK2%K:XFE70*LP$V25$0Q:J:4MO1P0%0L0HD+9E/HY+4J6TH48S%4K.GJ2PT3QY:GQ3TE2I+-CPHN6D7LLK*2HG%89UV-0LZ 2ZJJ524-LH/CJTK96L6SR9MU9DHGZ%P WUQRENS431T1XCNCF+47AY0-IFO0500TGPN8F5G.41Q2E4T8ALW.INSV$ 07UV5SR+BNQHNML7 /KD3TU 4V*CAT3ZGLQMI/XI%ZJNSBBXK2:UG%UJMI:TU+MMPZ5$/PMX19UE:-PSR3/$NU44CBE6DQ3D7B0FBOFX0DV2DGMB$YPF62I$60/F$Z2I6IFX21XNI-LM%3/DF/U6Z9FEOJVRLVW6K$UG+BKK57:1+D10%4K83F+1VWD1NE"

const b45data = exampleQR.replace("HC1:", "")
const zlibdata = base45.decode(b45data)
const cbor_cwt = pako.inflate(zlibdata)
const cwt = cbor.decodeFirstSync(cbor_cwt)
const payload = cbor.decodeFirstSync(cwt.value[2])

console.log(payload)

```

## Dependencies

Package.json format:

```
"base45": "^3.0.0",
"cbor-web": "^8.0.1", // for browsers, cbor for node-js
"pako": "^2.0.4",
```



