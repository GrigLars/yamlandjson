# YAML and JSON
My study of YAML and JSON

I got problems.  I am trying to figure out a lot of YAML and JSON and I can't find any online help that helps.  Maybe this will help someone else.  Maybe not.  This will expose how dumb I am, but it's worth it if I make someone's day.  You'll need access to a command line with "jq" a wonderful parser.  You install it with apt-get or yum or whatever your Linux distro uses.  Thanks goes to this site: https://onlineyamltools.com/convert-yaml-to-json

#### Here's some YAML I made up:

    foo:
      bar:
       - baz
       - biff
       - xyzzy
      bong:
       - bing
       - boof
    plugh:
      - dink
      - donk:
          - derp
          - nudoy: 
              durr
      - dolamite
    bixby:
      drop:
        drill:
         crabbo:
           - stabbo
           - stompo
    buzz: bats
    fuzz: cats
    
#### Here's the same thing in JSON:

    {
      "foo": {
        "bar": [
          "baz",
          "biff",
          "xyzzy"
        ],
        "bong": [
          "bing",
          "boof"
        ]
      },
      "plugh": [
        "dink",
        {
          "donk": [
            "derp",
            {
              "nudoy": "durr"
            }
          ]
        },
        "dolamite"
      ],
      "bixby": {
        "drop": {
          "drill": {
            "crabbo": [
              "stabbo",
              "stompo"
            ]
          }
        }
      },
      "buzz": "bats",
      "fuzz": "cats"
    }

So, using jq, I started messing with it.  I wanted to have a conversion or understanding in my head, "how does the YAML translate to JSON?"  Like, is there a one-to-one translation? It seems most start out with a "dot" like, "foo" for example:

    cat ~/json.json | jq .foo
    {
      "bar": [
        "baz",
        "biff",
        "xyzzy"
      ],
      "bong": [
        "bing",
        "boof"
      ]
    }

It seems like the "colon lines" are "headers" which are separated by "dots."  Note, these are my terms for the moment.  I am sure they are officially called fancier and more obfuscated things like "multi index register array objects" or something.

    cat ~/json.json | jq .bixby.drop
    {
      "drill": {
        "crabbo": [
          "stabbo",
          "stompo"
        ]
      }
    }

    cat ~/json.json | jq .bixby.drop.drill.crabbo
    [
      "stabbo",
      "stompo"
    ]

In this case, .bixby.drop.drill.crabbo is a "header" for an array consisting of two elements.

    cat ~/json.json | jq .bixby.drop.drill.crabbo[0]
    "stabbo"

    cat ~/json.json | jq .bixby.drop.drill.crabbo[]
    "stabbo"
    "stompo"

    cat ~/json.json | jq .bixby.drop.drill.crabbo[*]
    jq: error: syntax error, unexpected '*' (Unix shell quoting issues?) at <top-level>, line 1:
    .bixby.drop.drill.crabbo[*]                         
    jq: 1 compile error

So to get all the elements in an array, I call empty brackets, and not a wildcard. But whatabout "top level headers?"  I think they are really called "keys" becaise I found this:

    cat ~/json.json | jq -r keys
    [
      "bixby",
      "buzz",
      "foo",
      "fuzz",
      "plugh"
    ]

