# YAML and JSON
My study of YAML and JSON

I got problems.  I am trying to figure out a lot of YAML and JSON and I can't find any online help that helps.  Maybe this will help someone else.  Maybe not.  This will expose how dumb I am, but it's worth it if I make someone's day.  You'll need access to a command line with "jq" a wonderful parser.  You install it with apt-get or yum or whatever your Linux distro used.

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
          - nudoy           
      - dolamite            
    bixby:                  
      drop:                 
        drill:              
         crabbo:            
           - stabbo         
           - stompo         
           
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
            "nudoy"
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
      }
    }
