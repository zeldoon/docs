# Ready to make XCM Locations more human friendly? 👨‍🏫

This documentation provides you with all the steps necessary to implement core XCM Analyser functions. It also provides you with handy examples that can help you understand how to use this tool to its fullest potential.

## Implementation

> [!NOTE]
>The following junction types are supported:
>
>- Parachain
>- AccountId32
>- AccountIndex64
>- AccountKey20
>- PalletInstance
>- GeneralIndex
>- GeneralKey
>- OnlyChild
>- Plurality
>- GlobalConsensus

#### Compile a single location object to the URL

To compile a single location object to the URL, use the following structure:

```ts
//Importing the call
import { convertLocationToUrl } from '@paraspell/xcm-analyser';

//Define the location you wish to convert to URL
/*const location: Location = {
      parents: 0,
      interior: {
        X2: [
          {
            PalletInstance: 50,
          },
          {
            GeneralIndex: '41',
          },
        ],
      },
    };*/

const result = convertLocationToUrl(location);

/*
This should result into:
'./PalletInstance(50)/GeneralIndex(41)'
*/
```

#### Compile a single location JSON to the URL
To compile a single location JSON to the URL, use the following structure:

```ts
//Importing the call
import { convertLocationToUrlJson } from '@paraspell/xcm-analyser';

//Define location JSON
/*const locationJson = `{
      "parents": 3,
      "interior": {
        "X2": [
          {
            "PalletInstance": 50
          },
          {
            "GeneralIndex": "41"
          }
        ]
      }
    }`*/

const result = convertLocationToUrlJson(locationJson);

/*
This should result into:
''../../../PalletInstance(50)/GeneralIndex(41)''
*/
```

#### Compile the entire XCM call to the URL
To compile the entire XCM call to the URL, use the following structure:

```ts
//Importing the call
import { convertXCMToUrls } from '@paraspell/xcm-analyser';

//Define XCM call arguments you wish to convert
/*const xcmCallArguments = [
  {
    V3: {
      parents: 1,
      interior: {
        X1: {
          Parachain: 2006,
        },
      },
    },
  },
  {
    V3: {
      parents: 0,
      interior: {
        X1: {
          AccountId32: {
            network: null,
            id: '0xd43593c715fdd31c61141abd04a99fd6822c8558854ccde39a5684e7a56da27d',
          },
        },
      },
    },
  },
  {
    V3: [
      {
        id: {
          Concrete: {
            parents: 0,
            interior: {
              X2: [{ PalletInstance: 50 }, { GeneralIndex: '1984' }],
            },
          },
        },
        fun: {
          Fungible: 'amount',
        },
      },
    ],
  },
];*/

const urls = convertXCMToUrls(xcmCallArguments);

/*
This should result into:
[
  '../Parachain(2006)',
  './AccountId32(null, 0xd43593c715fdd31c61141abd04a99fd6822c8558854ccde39a5684e7a56da27d)',
  './PalletInstance(50)/GeneralIndex(1984)',
]
*/
```