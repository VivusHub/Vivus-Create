# Synopsis

Vivus Hub family of apps is designed to helps users create and share live experiences. This repo has been fully documented to the best of our knowledge to help both organisers and developers get the best experience from our platform. If you need further help in any section please feel free to email us at support@vivushub.com.

# Getting started
This documentation assumes you already have an API access token or key, if you don't have one please login to [Vivus](https://www.vivushub.com/vivus/interface/settings?ref=github). You'll find your token under settings.

```
    $action = "ActionType";
    $key = "AccessToken";
    $username = "Username";
    
    // example url -> https://www.vivushub.com/vivus/interface/API/public/eventlist/key/demo
    $ch = curl_init("https://www.vivushub.com/vivus/interface/API/public/$action/$key/$username");
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    $result = curl_exec($ch);
    
    // Set the parameters for arrays
    $id = array();
    $eventname = array();
    $description = array();


    // Clear json file and print it in text format
    // source [https://stackoverflow.com/questions/4343596/parsing-json-file-with-php]
    $jsonIterator = new RecursiveIteratorIterator(
    new RecursiveArrayIterator(json_decode($result, TRUE)),
    RecursiveIteratorIterator::SELF_FIRST);

    // Used for looping an other actions as seen below
    // You can remove this section but this was widely
    // implemented by other developers
    $x = 0;

    // Loop through post provided by each outlet
    foreach ($jsonIterator as $key => $val) {
        if(is_array($val)) {} 
        else {
        if($key == "id"){
            array_push($id, $val);
        }
        if($key == "eventname"){
            array_push($eventname, $val);
        }
        if($key == "details"){
            array_push($description, $val);
        }
    }
        // Looping vars
        $x = $x + 1;
    }


    // array size of the news
    $arraySize = sizeof($id);

    // Then loop through them
    for ($x = 0; $x < $arraySize; $x++) {

    // To output results e.g eventname
    echo("<h3>" . $eventname[$x] . "</h3>");
    echo("<p>" . $description[$x] . "</p>");
    
    // Link to the event
    echo("<p><a href='https://www.vivushub.com/vivus/interface/eventpage?ei="
    . $id[$x] . "'>Here</a></p>");
    }
    
```

The `$action`, `$key` and `$username` are the key parameters needed to make a successful query:

* `$action` - This variable states what information you may need, more examples:
  - eventlist: To get information of events hosted by you (the user).
  - eventvid: To get url link to videos upload to the Checkmate Vivus.
  - gallery: To get galleries of images uploaded to the Checkmate Vivus.
* `$key` - This is your unique identifier which can be found under settings, for public use you can use 'key' but access may be restricted.
* `$username` - This states whose information you would like to access (in most cases it is the information tailored to your access to token).

If successful the query returns a series of information in json format:

```
[
  {
    "id": "95",
    "username": "Vivus Hub",
    "eventname": "Lorem ipsum",
    "img": "https://www.vivushub.com/vivus/urlToImage.png",
    "memberPrice": "0",
    "price": "34",
    "tprice": "1",
    "details": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur nulla tortor, mollis at tristique ut, iaculis ut justo. Pellentesque eu ultricies orci. Vestibulum quis lorem blandit, euismod lectus quis, maximus augue. Nulla mi purus, ultricies viverra sem nec, venenatis molestie lacus. Quisque id fermentum nulla, vel vehicula ex. In quis.",
    "views": "0",
    "location": "Manchester, United Kingdom",
    "sold": "41",
    "date": "2018-06-01",
    "eventid": "1b5691b395abd7330b0a5cffac41abe6"
  }
]

```
The Vivus Hub has several request endpoints from viewing your listed events or just creating events. 

We’ve documented a bulk of it in the link below but as they say if you know one you know them all but do check how we accept data entry and data request.
- Organisers:
  - [Event List](https://github.com/VivusHub/Vivus-Create/blob/master/sdk-php/eventlist.md)
  - [Create Event](https://github.com/VivusHub/Vivus-Create/blob/master/sdk-php/createEvent.md)

# Credits

Vivus Hub API is owned and maintained by [Vivus Hub ltd](https://www.vivushub.com/vivus/?ref=github&adFor=events). You can follow us on Twitter at [VivusHub](https://www.twitter.com/vivushub) to get project updates or fork this repo.

# License

The codes and all related text in this documentation falls under [Vivus Hub Content and Commercially available contents licence agreement](https://www.vivushub.com/vivus/interface/terms)
