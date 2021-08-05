# Algorithm Generated NFT

## Modeling

SpacePanda base modal was built on top of [blender](https://www.blender.org/)

## Body Parts Generation

Once the modeling of SpacePanda is done. It will output the SVG format of the base SpacePanda. Then the SpacePanda generation algorithm will run in TEE to produce an unique NFT for user. Here is an example how the eyes are generated. **randomEye** function will receive a rand parameter to create random eyes for SpacePanda. Please note that the rand parameter is a seed random number generated in TEE.

```javascript
function randomEye(panda: Panda, rand): Panda {
    // eye circle
    const offsetX = rand.intBetween(0, 17) - 7; // max is 10, min is -7
    const offsetY = rand.intBetween(0, 30) - 10; // max is 20, min is -10
    const angle = rand.intBetween(0, 60) - 20; // -20 ~ 40 deg

    changeTransform(panda.svg, `translate(${0 - offsetX}, ${0 - offsetY}) rotate(${angle}, 285 217)`, 'transfer-reye');
    changeTransform(panda.svg, `translate(${offsetX}, ${0 - offsetY}) rotate(${0 - angle}, 96 217)`, 'transfer-leye');
    // eye scale first
    const leftEyeCentX = 119;
    const rightEyeCentX = 264;
    const eyeCentY = 213;
    const eyeRatio: any = (rand.intBetween(75, 100) / 100).toFixed(2);

    // update position when scale
    const offsetXt = rand.intBetween(0, 13) - 10; // min is -10, max is 3
    const offsetYt = rand.intBetween(0, 20) - 10;
    changeTransform(panda.svg, `translate(${_.round((1 - eyeRatio) * leftEyeCentX) + offsetXt}, ${_.round((1 - eyeRatio) * eyeCentY) - offsetYt}) scale(${eyeRatio})`, 'transfer-ltong');
    changeTransform(panda.svg, `translate(${_.round((1 - eyeRatio) * rightEyeCentX) - offsetXt}, ${_.round((1 - eyeRatio) * eyeCentY) - offsetYt}) scale(${eyeRatio})`, 'transfer-rtong');

    // eye highlight and scale
    changeTransform(panda.svg, `translate(${_.round((1 - eyeRatio) * leftEyeCentX) + offsetXt}, ${_.round((1 - eyeRatio) * eyeCentY) - offsetYt}) scale(${eyeRatio})`, 'transfer-ltong-light');
    changeTransform(panda.svg, `translate(${_.round((1 - eyeRatio) * rightEyeCentX) - offsetXt}, ${_.round((1 - eyeRatio) * eyeCentY) - offsetYt}) scale(${eyeRatio})`, 'transfer-rtong-light');

    panda.eye_circle_shape = {
        x: offsetX,
        y: offsetY,
        angle
    };
    panda.eyes.shape = {
        x: offsetXt,
        y: offsetYt,
        scale: eyeRatio * 100
    };
    return panda;
}
```



## IPFS Integration

The generated SpacePanda NFT will be stored on IPFS. The following sample scripts shows how the SpacePanda artifacts are stored on IPFS:

```javascript
import { getPanda } from './file-util';
import { logger } from '../config/logger';
import { PINATA_API_KEY, PINATA_API_SECRET } from '../config/config';

const axios = require('axios');
const fs = require('fs');
const FormData = require('form-data');

export const pinFileToIPFS = (id) => {
  const url = `https://api.pinata.cloud/pinning/pinFileToIPFS`;
  let data = new FormData();
  data.append('file', fs.createReadStream(getPanda(id, true)));

  const metadata = JSON.stringify({
    name: `SpacePanda #${id}`,
    keyvalues: {}
  });
  data.append('pinataMetadata', metadata);

  //pinataOptions are optional
  const pinataOptions = JSON.stringify({
    cidVersion: 0,
    customPinPolicy: {
      regions: [
        {
          id: 'FRA1',
          desiredReplicationCount: 2
        },
        {
          id: 'NYC1',
          desiredReplicationCount: 2
        }
      ]
    }
  });
  data.append('pinataOptions', pinataOptions);

  return axios
    .post(url, data, {
      maxBodyLength: 'Infinity',
      headers: {
        'Content-Type': `multipart/form-data; boundary=${data._boundary}`,
        pinata_api_key: PINATA_API_KEY,
        pinata_secret_api_key: PINATA_API_SECRET
      }
    })
    .catch(function (error) {
      logger.error(`failed to upload to ipfs for ${id} with error: ${error.toString()}`)
    });
};

```

