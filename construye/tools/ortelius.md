# API de Ortelius

### descripción: "Esta API permite a los clientes interactuar con Ortelius, el indexador de Avalanche".

## API de Ortelius

### API de Ortelius

#### Formato

Esta API usa peticiones GET HTTP usando parámetros de consulta de URL y devuelve los datos de JSON.

Versionado

A partir de la versión 2, las rutas de la API serán precedidas por una etiqueta de versión, por ejemplo, `http://localhost:8080/v2`.

La versión actual de la API es la versión 2. La documentación de la [API Legacy ](ortelius.md#legacy-api) contiene información sobre el uso de la API v1.

Tipos de datos

Además de los números enteros, las cadenas y los booleanos, se utilizan los siguientes tipos de datos en toda la API:

| Nombre | Descripción | Ejemplos |
| :--- | :--- | :--- |
| `id` | Un identificador de objeto codificado CB58, como una cadena, una transacción o una identificación de activo | `2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM` |
| `address` | Una dirección codificada bech-32 | `fuji1wycv8n7d2fg9aq6unp23pnj4q0arv03ysya8jw` |
| `datetime` | Una timestamp de Unix como un entero o una cadena con formato RFC3339 | `1599696000`, `2020-09-10T00:00:00Z` |

#### Parámetros de la Lista

Todos los puntos finales de la lista de recursos aceptan los siguientes parámetros:

| Nombre | Tipo | Descripción | Default | Max |
| :--- | :--- | :--- | :--- | :--- |
| `limit` | `int` | El número máximo de elementos a enviar | `500` | `500` |
| `offset` | `int` | El número de elementos a omitir | `0` | None |
| `query` | `string` | Un prefijo de ID para filtrar los elementos. | None | None |
| `startTime` | `datetime` | Límites a los elementos creados en o después de un tiempo determinado | `0` | Now |
| `endTime` | `datetime` | Límites a los elementos creados en o antes de un tiempo determinado | Now | Now |

#### Endpoints Disponibles

**Resumen**

La raíz de la API da una visión general de las constantes de la red activa de Avalanche que se está indexando.

**Parámetros**

Ninguno

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2"
```

**Respuesta de Ejemplo**

```javascript
{
  "network_id": 1,
  "chains": {
    "11111111111111111111111111111111LpoYY": {
      "chainID": "11111111111111111111111111111111LpoYY",
      "chainAlias": "p",
      "vm": "pvm",
      "avaxAssetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
      "networkID": 1
    },
    "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM": {
      "chainID": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
      "chainAlias": "x",
      "vm": "avm",
      "avaxAssetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
      "networkID": 1
    }
  }
}
```

**Buscar**

Encuentra una dirección o una transacción por su ID.

**Parámetros**

| Nombre | Tipo | Descripción | Default | Max |
| :--- | :--- | :--- | :--- | :--- |
| `query` | `string` | Un prefijo de ID para filtrar los elementos. | None | None |

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/search?query=2jEugPDFN89KXLEXtf5"
```

**Respuesta de Ejemplo**

```javascript
{
  "count": 1,
  "results": [
    {
      "type": "transaction",
      "data": {
        "id": "2jEugPDFN89KXLEXtf5oKp5spsJawTht2zP4kKJjkQwwRsDdLX",
        "chainID": "11111111111111111111111111111111LpoYY",
        "type": "add_validator",
        "inputs": [
          {
            "output": {
              "id": "G2Jq9fj6atW1jvJDTXJKHSkMhRWdrsFuafPpR98DK3izZdfqT",
              "transactionID": "11111111111111111111111111111111LpoYY",
              "outputIndex": 14025,
              "assetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
              "outputType": 7,
              "amount": "2000000000000",
              "locktime": 0,
              "threshold": 1,
              "addresses": [
                "avax14q43wu6wp8fs745dt6y5s0a02vx57ypq4xc5s3"
              ],
              "timestamp": "2020-09-10T00:00:00Z",
              "redeemingTransactionID": "2jEugPDFN89KXLEXtf5oKp5spsJawTht2zP4kKJjkQwwRsDdLX"
            },
            "credentials": [
              {
                "address": "avax14q43wu6wp8fs745dt6y5s0a02vx57ypq4xc5s3",
                "public_key": "AgSmTeCLGsNhKvSbRIi01jswlr2fV+C/tv3v86Ty4eDQ",
                "signature": "Ms5KquahoTfLGeIl5s6iP5r1fj15lm5MmrMahu8X7L0m5UTyRBRmcXnniURFaJP6X8dCL9f46t8zYawXscdgkQE="
              }
            ]
          }
        ],
        "outputs": [
          {
            "id": "U7M4jk3y7KGWPmSoeS4WhBX6qNHGtkDtQ5dSzYiaw4rmZ92yE",
            "transactionID": "2jEugPDFN89KXLEXtf5oKp5spsJawTht2zP4kKJjkQwwRsDdLX",
            "outputIndex": 0,
            "assetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
            "outputType": 7,
            "amount": "2000000000000",
            "locktime": 0,
            "threshold": 1,
            "addresses": [
              "avax14q43wu6wp8fs745dt6y5s0a02vx57ypq4xc5s3"
            ],
            "timestamp": "2020-10-10T07:09:44Z",
            "redeemingTransactionID": ""
          }
        ],
        "memo": "AAAAAA==",
        "inputTotals": {
          "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": "2000000000000"
        },
        "outputTotals": {
          "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": "2000000000000"
        },
        "reusedAddressTotals": null,
        "timestamp": "2020-10-10T07:09:44Z",
        "txFee": 0,
        "genesis": false
      },
      "score": 0
    }
  ]
}
```

**Agregado**

Calcular los datos agregados de las transacciones a lo largo de un período de tiempo.

**Parámetros**

| Nombre | Tipo | Descripción | Default | Max |
| :--- | :--- | :--- | :--- | :--- |
| `chainID` | `id` | Un ID en cadena para filtrar los resultados. Puede ser suministrado varias veces. | None | None |
| `assetID` | `id` | Una ID de activos para filtrar los resultados.. | None | None |

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/aggregates?startTime=2020-09-21T00:00:00Z&endTime=2020-10-21T00:00:00Z"
```

**Respuesta de Ejemplo**

```javascript
{
  "startTime": "2020-09-21T00:00:00Z",
  "endTime": "2020-10-21T00:00:00Z",
  "aggregates": {
    "startTime": "2020-09-21T00:00:00Z",
    "endTime": "2020-10-21T00:00:00Z",
    "transactionVolume": "1652211194850792239",
    "transactionCount": 135966,
    "addressCount": 19567,
    "outputCount": 283221,
    "assetCount": 180
  }
}
```

**Agregado TxFee**

Agregado AVAX txfee

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/txfeeAggregates?startTime=2020-09-21T00:00:00Z&endTime=2020-10-21T00:00:00Z"
```

**Respuesta de Ejemplo**

```javascript
{
  "aggregates": {
    "startTime": "2020-09-21T00:00:00Z",
    "endTime": "2020-10-21T00:00:00Z",
    "txfee": "134818000000"
  },
  "startTime": "2020-09-21T00:00:00Z",
  "endTime": "2020-10-21T00:00:00Z"
}
```

**Cadena de Direcciones**

Responde con las cadenas en las que aparece una dirección

**Parámetros**

| Nombre | Tipo | Descripción | Default | Max |
| :--- | :--- | :--- | :--- | :--- |
| `address` | `address` | Una dirección para filtrar los resultados. Puede ser suministrada varias veces. | None | None |

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/addressChains?address=X-fujiABC"
```

**Respuesta de Ejemplo**

```javascript
{
  "addressChains": {
    "avax14q43wu6wp8fs745dt6y5s0a02vx57ypq4xc5s3": [
      "11111111111111111111111111111111LpoYY"
    ],
    "avax1y8cyrzn2kg4udccs5d625gkac7a99pe452cy5u": [
      "11111111111111111111111111111111LpoYY",
      "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM"
    ]
  }
}
```

**Lista de transacciones**

Encuentra transacciones confirmadas de la red.

**Parámetros**

| Nombre | Tipo | Descripción | Default | Max |
| :--- | :--- | :--- | :--- | :--- |
| `chainID` | `id` | Una ID en cadena para filtrar los resultados. Puede ser suministrada varias veces. | None | None |
| `assetID` | `id` | Una ID de activos para filtrar los resultados. | None | None |
| `address` | `address` | Una dirección por la que filtrar los resultados. Puede ser suministrada varias veces. | None | None |
| `disableGenesis` | `bool` | Cuando sea true, los datos del vértice del Génesis no retornan. | true | N/A |
| `sort` | `string` | Un método para clasificar los resultados. Puede ser `timestamp-asc` o`timestamp-desc`. | `timestamp-asc` | N/A |

**Llamado de Ejemplo**

```bash
curl "http://localhost:8080/v2/transactions?limit=1&chainID=11111111111111111111111111111111LpoYY&offset=100"
```

**Respuesta de Ejemplo**

```javascript
{
  "startTime": "0001-01-01T00:00:00Z",
  "endTime": "2020-11-16T04:18:07Z",
  "transactions": [
    {
      "id": "2jEugPDFN89KXLEXtf5oKp5spsJawTht2zP4kKJjkQwwRsDdLX",
      "chainID": "11111111111111111111111111111111LpoYY",
      "type": "add_validator",
      "inputs": [
        {
          "output": {
            "id": "G2Jq9fj6atW1jvJDTXJKHSkMhRWdrsFuafPpR98DK3izZdfqT",
            "transactionID": "11111111111111111111111111111111LpoYY",
            "outputIndex": 14025,
            "assetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
            "outputType": 7,
            "amount": "2000000000000",
            "locktime": 0,
            "threshold": 1,
            "addresses": [
              "avax14q43wu6wp8fs745dt6y5s0a02vx57ypq4xc5s3"
            ],
            "timestamp": "2020-09-10T00:00:00Z",
            "redeemingTransactionID": "2jEugPDFN89KXLEXtf5oKp5spsJawTht2zP4kKJjkQwwRsDdLX"
          },
          "credentials": [
            {
              "address": "avax14q43wu6wp8fs745dt6y5s0a02vx57ypq4xc5s3",
              "public_key": "AgSmTeCLGsNhKvSbRIi01jswlr2fV+C/tv3v86Ty4eDQ",
              "signature": "Ms5KquahoTfLGeIl5s6iP5r1fj15lm5MmrMahu8X7L0m5UTyRBRmcXnniURFaJP6X8dCL9f46t8zYawXscdgkQE="
            }
          ]
        }
      ],
      "outputs": [
        {
          "id": "U7M4jk3y7KGWPmSoeS4WhBX6qNHGtkDtQ5dSzYiaw4rmZ92yE",
          "transactionID": "2jEugPDFN89KXLEXtf5oKp5spsJawTht2zP4kKJjkQwwRsDdLX",
          "outputIndex": 0,
          "assetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
          "outputType": 7,
          "amount": "2000000000000",
          "locktime": 0,
          "threshold": 1,
          "addresses": [
            "avax14q43wu6wp8fs745dt6y5s0a02vx57ypq4xc5s3"
          ],
          "timestamp": "2020-10-10T07:09:44Z",
          "redeemingTransactionID": ""
        }
      ],
      "memo": "AAAAAA==",
      "inputTotals": {
        "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": "2000000000000"
      },
      "outputTotals": {
        "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": "2000000000000"
      },
      "reusedAddressTotals": null,
      "timestamp": "2020-10-10T07:09:44Z",
      "txFee": 0,
      "genesis": false
    }
  ]
}
```

**Obtener Transacción**

Encuentra una transacción por su ID.

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/transactions/2jEugPDFN89KXLEXtf5oKp5spsJawTht2zP4kKJjkQwwRsDdLX"
```

**Respuesta de Ejemplo**

```javascript
{
  "id": "2jEugPDFN89KXLEXtf5oKp5spsJawTht2zP4kKJjkQwwRsDdLX",
  "chainID": "11111111111111111111111111111111LpoYY",
  "type": "add_validator",
  "inputs": [
    {
      "output": {
        "id": "G2Jq9fj6atW1jvJDTXJKHSkMhRWdrsFuafPpR98DK3izZdfqT",
        "transactionID": "11111111111111111111111111111111LpoYY",
        "outputIndex": 14025,
        "assetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
        "outputType": 7,
        "amount": "2000000000000",
        "locktime": 0,
        "threshold": 1,
        "addresses": [
          "avax14q43wu6wp8fs745dt6y5s0a02vx57ypq4xc5s3"
        ],
        "timestamp": "2020-09-10T00:00:00Z",
        "redeemingTransactionID": "2jEugPDFN89KXLEXtf5oKp5spsJawTht2zP4kKJjkQwwRsDdLX"
      },
      "credentials": [
        {
          "address": "avax14q43wu6wp8fs745dt6y5s0a02vx57ypq4xc5s3",
          "public_key": "AgSmTeCLGsNhKvSbRIi01jswlr2fV+C/tv3v86Ty4eDQ",
          "signature": "Ms5KquahoTfLGeIl5s6iP5r1fj15lm5MmrMahu8X7L0m5UTyRBRmcXnniURFaJP6X8dCL9f46t8zYawXscdgkQE="
        }
      ]
    }
  ],
  "outputs": [
    {
      "id": "U7M4jk3y7KGWPmSoeS4WhBX6qNHGtkDtQ5dSzYiaw4rmZ92yE",
      "transactionID": "2jEugPDFN89KXLEXtf5oKp5spsJawTht2zP4kKJjkQwwRsDdLX",
      "outputIndex": 0,
      "assetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
      "outputType": 7,
      "amount": "2000000000000",
      "locktime": 0,
      "threshold": 1,
      "addresses": [
        "avax14q43wu6wp8fs745dt6y5s0a02vx57ypq4xc5s3"
      ],
      "timestamp": "2020-10-10T07:09:44Z",
      "redeemingTransactionID": ""
    }
  ],
  "memo": "AAAAAA==",
  "inputTotals": {
    "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": "2000000000000"
  },
  "outputTotals": {
    "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": "2000000000000"
  },
  "reusedAddressTotals": null,
  "timestamp": "2020-10-10T07:09:44Z",
  "txFee": 0,
  "genesis": false
}
```

**Lista de direcciones**

Encuentra las direcciones que han estado involucradas en transacciones confirmadas.

**Parámetros**

| Nombre | Tipo | Descripción | Default | Max |
| :--- | :--- | :--- | :--- | :--- |
| `chainID` | `id` | Una ID en cadena para filtrar los resultados. Puede ser suministrada varias veces. | None | None |
| `address` | `address` | Una dirección para filtrar los resultados. Puede ser suministrada varias veces. | None | None |

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/addresses?limit=1"
```

**Respuesta de Ejemplo**

```javascript
{
  "addresses": [
    {
      "address": "avax1y8cyrzn2kg4udccs5d625gkac7a99pe452cy5u",
      "publicKey": null,
      "assets": {
        "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": {
          "id": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
          "transactionCount": 2,
          "utxoCount": 17,
          "balance": "39561999999996",
          "totalReceived": "39561999999996",
          "totalSent": "0"
        }
      }
    }
  ]
}
```

**Obtener Dirección**

Encuentra una dirección por su ID.

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/addresses/avax1y8cyrzn2kg4udccs5d625gkac7a99pe452cy5u"
```

**Respuesta de Ejemplo**

```javascript
{
  "address": "avax1y8cyrzn2kg4udccs5d625gkac7a99pe452cy5u",
  "publicKey": null,
  "assets": {
    "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z": {
      "id": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
      "transactionCount": 2,
      "utxoCount": 17,
      "balance": "39561999999996",
      "totalReceived": "39561999999996",
      "totalSent": "0"
    }
  }
}
```

**Lista de activos**

Encuentra activos que se han creado en la X-chain.

**Parámetros**

| Nombre | Tipo | Descripción | Default | Max |
| :--- | :--- | :--- | :--- | :--- |
| `enableAggregate` | string | Los valores "minute", "hour", "day", "week", "month", or "year" cuando se proporcionen, se incluirán datos agregados sobre el activo. | N/A | N/A |

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/assets?limit=1&enableAggregate=minute"
```

**Respuesta de Ejemplo**

```javascript
{
  "assets": [
    {
      "id": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
      "chainID": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
      "name": "Avalanche",
      "symbol": "AVAX",
      "alias": "AVAX",
      "currentSupply": "24509771588234718",
      "timestamp": "2020-09-10T00:00:00Z",
      "denomination": 9,
      "variableCap": 0,
      "aggregates": {
        "day": {
          "startTime": "2020-11-15T04:47:00Z",
          "endTime": "2020-11-16T04:47:00Z",
          "transactionVolume": "0",
          "transactionCount": 0,
          "addressCount": 0,
          "outputCount": 0,
          "assetCount": 0
        },
        "hour": {
          "startTime": "2020-11-16T03:47:00Z",
          "endTime": "2020-11-16T04:47:00Z",
          "transactionVolume": "0",
          "transactionCount": 0,
          "addressCount": 0,
          "outputCount": 0,
          "assetCount": 0
        },
        "minute": {
          "startTime": "2020-11-16T04:46:00Z",
          "endTime": "2020-11-16T04:47:00Z",
          "transactionVolume": "0",
          "transactionCount": 0,
          "addressCount": 0,
          "outputCount": 0,
          "assetCount": 0
        },
        "month": {
          "startTime": "2020-10-17T04:47:00Z",
          "endTime": "2020-11-16T04:47:00Z",
          "transactionVolume": "0",
          "transactionCount": 0,
          "addressCount": 0,
          "outputCount": 0,
          "assetCount": 0
        },
        "week": {
          "startTime": "2020-11-09T04:47:00Z",
          "endTime": "2020-11-16T04:47:00Z",
          "transactionVolume": "0",
          "transactionCount": 0,
          "addressCount": 0,
          "outputCount": 0,
          "assetCount": 0
        },
        "year": {
          "startTime": "2019-11-17T04:47:00Z",
          "endTime": "2020-11-16T04:47:00Z",
          "transactionVolume": "6637657099999996",
          "transactionCount": 1,
          "addressCount": 159,
          "outputCount": 1,
          "assetCount": 817
        }
      }
    }
  ]
}
```

**Obtener Activo**

Encuentra un activo por su ID.

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/assets/FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z?enableAggregate=true"
```

**Respuesta de Ejemplo**

```javascript
{
  "id": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
  "chainID": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
  "name": "Avalanche",
  "symbol": "AVAX",
  "alias": "AVAX",
  "currentSupply": "24509771588234718",
  "timestamp": "2020-09-10T00:00:00Z",
  "denomination": 9,
  "variableCap": 0,
  "aggregates": {
    "day": {
      "startTime": "2020-11-15T04:50:00Z",
      "endTime": "2020-11-16T04:50:00Z",
      "transactionVolume": "0",
      "transactionCount": 0,
      "addressCount": 0,
      "outputCount": 0,
      "assetCount": 0
    },
    "hour": {
      "startTime": "2020-11-16T03:50:00Z",
      "endTime": "2020-11-16T04:50:00Z",
      "transactionVolume": "0",
      "transactionCount": 0,
      "addressCount": 0,
      "outputCount": 0,
      "assetCount": 0
    },
    "minute": {
      "startTime": "2020-11-16T04:49:00Z",
      "endTime": "2020-11-16T04:50:00Z",
      "transactionVolume": "0",
      "transactionCount": 0,
      "addressCount": 0,
      "outputCount": 0,
      "assetCount": 0
    },
    "month": {
      "startTime": "2020-10-17T04:50:00Z",
      "endTime": "2020-11-16T04:50:00Z",
      "transactionVolume": "0",
      "transactionCount": 0,
      "addressCount": 0,
      "outputCount": 0,
      "assetCount": 0
    },
    "week": {
      "startTime": "2020-11-09T04:50:00Z",
      "endTime": "2020-11-16T04:50:00Z",
      "transactionVolume": "0",
      "transactionCount": 0,
      "addressCount": 0,
      "outputCount": 0,
      "assetCount": 0
    },
    "year": {
      "startTime": "2019-11-17T04:50:00Z",
      "endTime": "2020-11-16T04:50:00Z",
      "transactionVolume": "6637657099999996",
      "transactionCount": 1,
      "addressCount": 159,
      "outputCount": 1,
      "assetCount": 817
    }
  }
}
```

**Lista de salidas**

Encontrar salidas que hayan sido creadas por una transacción confirmada en la red.

**Parámetros**

| Nombre | Tipo | Descripción | Default | Max |
| :--- | :--- | :--- | :--- | :--- |
| `chainID` | `id` | Una ID en cadena para filtrar los resultados. Puede ser suministrada varias veces. | None | None |
| `address` | `address` | Una dirección para filtrar los resultados. Puede ser suministrada varias veces. | None | None |
| `spent` | `bool` | Si se establece, los resultados serán filtrados por si se gastan \(true\) o no se gastan \(false\) | None | N/A |

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/outputs?limit=1&spent=false"
```

**Respuesta de Ejemplo**

```javascript
{
  "outputs": [
    {
      "id": "114RMPhYM7do7cDX7KWSqFeLkbUXFrLKcqPL4GMdjTvemPzvc",
      "transactionID": "dhU8aMRrtMWvBWSh41aTxUbwArYootNUBcL3N3UJXVPL8H9ip",
      "outputIndex": 4,
      "assetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
      "outputType": 7,
      "amount": "2327176470588",
      "locktime": 0,
      "threshold": 1,
      "addresses": [
        "avax1y8cyrzn2kg4udccs5d625gkac7a99pe452cy5u"
      ],
      "timestamp": "2020-09-10T00:00:00Z",
      "redeemingTransactionID": ""
    }
  ]
}
```

**Obtener Salida**

Encuentra una salida por su ID.

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/v2/outputs/114RMPhYM7do7cDX7KWSqFeLkbUXFrLKcqPL4GMdjTvemPzvc"
```

**Respuesta de Ejemplo**

```javascript
{
  "id": "114RMPhYM7do7cDX7KWSqFeLkbUXFrLKcqPL4GMdjTvemPzvc",
  "transactionID": "dhU8aMRrtMWvBWSh41aTxUbwArYootNUBcL3N3UJXVPL8H9ip",
  "outputIndex": 4,
  "assetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z",
  "outputType": 7,
  "amount": "2327176470588",
  "locktime": 0,
  "threshold": 1,
  "addresses": [
    "avax1y8cyrzn2kg4udccs5d625gkac7a99pe452cy5u"
  ],
  "timestamp": "2020-09-10T00:00:00Z",
  "redeemingTransactionID": ""
}
```

#### API Legacy

La versión 1 de la API fue construida para soportar sólo la X-chain, y no usaba un prefijo de versión \(`/v1`\). Está disponible en el directorio `/x` de la raíz, que es el endpoint de la visión general solamente para la X-chain:

**Llamado de Ejemplo**

```text
curl "http://localhost:8080/x"
```

**Respuesta de Ejemplo**

```javascript
{
  "networkID": 1,
  "vm": "avm",
  "chainAlias": "x",
  "chainID": "2oYMBNV4eNHyqk2fjjV5nVQLDbtmNJzq5s3qs3Lo6ftnC6FByM",
  "avaxAssetID": "FvwEAhmxKfeiG8SnEvq42hc6whRyY3EFYAvebMqDNDGCgxN5Z"
}
```

La API legacy admite los mismos endpoints y parámetros que la versión 2, excepto el parámetro chainID para todos los puntos finales, que se ajusta por defecto al ID de la X-chain.

### Configuración de Ortelius

Configuración usando un archivo JSON para las aplicaciones de Ortelius. La configuración define qué red y blockchains debe indexar Ortelius, así como la información de conexión para los servicios de respaldo requeridos.

### Ejemplo

Esta configuración es la que utiliza la configuración autónoma de Docker Compose e ilustra los diversos ajustes disponibles `kafka`, `mysql`, y`redis` son nombres de DNS que resuelven el servicio correspondiente.

```javascript
{
  "networkID": 5,
  "logDirectory": "/var/log/ortelius",
  "listenAddr": "localhost:8080",
  "chains": {
    "11111111111111111111111111111111LpoYY": {
      "id": "11111111111111111111111111111111LpoYY",
      "alias": "P",
      "vmType": "pvm"
    },
    "2JVSBoinj9C2J33VntvzYtVJNZdN2NKiwwKjcumHUWEb5DbBrm": {
      "id": "2JVSBoinj9C2J33VntvzYtVJNZdN2NKiwwKjcumHUWEb5DbBrm",
      "alias": "F",
      "vmType": "avm"
    }
  },
  "stream": {
    "kafka": {
      "brokers": [
        "kafka:9092"
      ]
    },
    "producer": {
        "ipcRoot": "/tmp"
    },
    "consumer": {
        "groupName": "indexer"
    }
  },
  "services": {
    "redis": {
      "addr": "redis:6379"
    },
    "db": {
      "dsn": "root:password@tcp(mysql:3306)/ortelius",
      "driver": "mysql"
    }
  }
}
```
