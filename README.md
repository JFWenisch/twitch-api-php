
# twitch-api-php

Goal of this project is to allow an easy access to twitch related channel information via the twitch api . At the point of creating this project all existing projects I found were either still migrating from the old API to helix or have been pretty heavyweight for just getting some twitch information. To use this project and query information you only need a client_id and client_secret which can be obtained after creating an account at https://dev.twitch.tv/console/apps/create . The app authenticates itself using the OAuth client credentials flow as described under https://dev.twitch.tv/docs/authentication/getting-tokens-oauth/#oauth-client-credentials-flow and returns relevant data as json

## Getting started
Clone this repo

    git clone https://github.com/JFWenisch/twitch-api-php.git

Create a file named "config.ini" in the root directory with the following content. Replace the clientid & clientsecret from  https://dev.twitch.tv/console and replace the channelname with your desired channel

    clientid = vb8l039xxxxxxxxxxxxxxxxx
    clientsecret = oubwxxxxxxxxxxxxxxxxxx
    channelname = auhuur_tv

Now we are ready to go. Having php installed yo should be able to spin up a server for test purposes using

    php -S localhost:8000
    
## Usage
To get the information you just need to make a GET request to the index.php while supplying the function which you want to use. So you will end up with a GET  `index.php?f=info` while 'info' can be replaced with whatever function you want to call. Currently implemented are


| function |example data  |
|--|--|
| info |`[{"broadcaster_language":"de","broadcaster_login":"auhuur_tv","display_name":"AuHuur_TV","game_id":"32399","id":"651531159","is_live":false,"tag_ids":[],"thumbnail_url":"https:\/\/static-cdn.jtvnw.net\/jtv_user_pictures\/cf834be8-05d2-4c00-91e3-2594f1f8e46a-profile_image-300x300.png","title":"Team Kohlscheid vs BootyBayBitches","started_at":""}]`  |
| topclips | `{"clips":[{"slug":"TemperedAgileTurtleANELE-VpcKBFZvEKcD_QQm","tracking_id":"1058659358","url":"https://clips.twitch.tv/TemperedAgileTurtleANELE-VpcKBFZvEKcD_QQm?tt_medium=clips_api\u0026tt_content=url","embed_url":"https://clips.twitch.tv/embed?clip=TemperedAgileTurtleANELE-VpcKBFZvEKcD_QQm\u0026tt_medium=clips_api\u0026tt_content=embed","embed_html":"\u003ciframe src='https://clips.twitch.tv/embed?clip=TemperedAgileTurtleANELE-VpcKBFZvEKcD_QQm\u0026tt_medium=clips_api\u0026tt_content=embed' width='640' height='360' frameborder='0' scrolling='no' allowfullscreen='true'\u003e\u003c/iframe\u003e","broadcaster":{"id":"651531159","name":"auhuur_tv","display_name":"AuHuur_TV","channel_url":"https://www.twitch.tv/auhuur_tv","logo":"https://static-cdn.jtvnw.net/jtv_user_pictures/cf834be8-05d2-4c00-91e3-2594f1f8e46a-profile_image-300x300.png"},"curator":{"id":"651531159","name":"auhuur_tv","display_name":"AuHuur_TV","channel_url":"https://www.twitch.tv/auhuur_tv","logo":"https://static-cdn.jtvnw.net/jtv_user_pictures/cf834be8-05d2-4c00-91e3-2594f1f8e46a-profile_image-150x150.png"},"vod":{"id":"920524678","url":"https://www.twitch.tv/videos/920524678?t=1h2m52s","offset":3772,"preview_image_url":"https://clips-media-assets2.twitch.tv/vod-920524678-offset-3800-preview.jpg"},"broadcast_id":"41159409724","game":"Escape From Tarkov","language":"de","title":"Best Teammate EU","views":34,"duration":30,"created_at":"2021-02-19T23:49:00Z","thumbnails":{"medium":"https://clips-media-assets2.twitch.tv/vod-920524678-offset-3800-preview-480x272.jpg","small":"https://clips-media-assets2.twitch.tv/vod-920524678-offset-3800-preview-260x147.jpg","tiny":"https://clips-media-assets2.twitch.tv/vod-920524678-offset-3800-preview-86x45.jpg"}}],"_cursor":""}` |





### Example Usage

Using curl

    PS C:\Users\user> curl 'http://localhost:8000/?f=info'
    
    
    StatusCode        : 200
    StatusDescription : OK
    Content           : [{"broadcaster_language":"de","broadcaster_login":"auhuur_tv","display_name":"AuHuur_TV","game_id":
                        "32399","id":"651531159","is_live":false,"tag_ids":[],"thumbnail_url":"https:\/\/static-cdn.jtvnw.n
                        et...
    RawContent        : HTTP/1.1 200 OK
                        Host: localhost:8000
                        Connection: close
                        Content-Type: text/html; charset=UTF-8
                        Date: Tue, 23 Feb 2021 16:13:31 GMT
                        X-Powered-By: PHP/8.0.2
    
                        [{"broadcaster_language":"de","broadca...
    Forms             : {}
    Headers           : {[Host, localhost:8000], [Connection, close], [Content-Type, text/html; charset=UTF-8], [Date,
                        Tue, 23 Feb 2021 16:13:31 GMT]...}
    Images            : {}
    InputFields       : {}
    Links             : {}
    ParsedHtml        : mshtml.HTMLDocumentClass
    RawContentLength  : 347

or using jquery / ajax

    $.get( "index.php?f=info", function( data ) {
      alert( "Data Loaded: " + data );
    });



## Deployment

In order to deploy this app just copy the index.php and config.ini to your server.
**IMPORTANT:** As your credentials are stored in the config.ini you should make sure that no one is able to access this file if you deploy it to your webserver. I have included a sample .htaccess file which can be used

    <files config.ini>
    order allow,deny
    deny from all
    </files>



