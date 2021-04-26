# trello-board-json-to-html-template


```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>True Trello Printer</title>
    <link href="http://netdna.bootstrapcdn.com/bootstrap/3.0.3/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            margin: 15%;
        }

        .panel-body {
            font-size: 1.2em;

        }
    </style>
    <STYLE type="text/css" media="print">
        body {
            margin: 0;
        }
    </STYLE>
</head>

<body>

    <div id="out">
        No Trello JSON data found
    </div>

    </ul>
    </div>

    <script type="text/html" id="template-output">
        {{#lists}}
        <h1> {{name}}</h1>
        {{#cards}}
        <div class="panel panel-default">
            <div class="panel-heading">
                <h4>{{name}}</h4>{{{desc}}}
            </div>
            <!--div class="panel-body" >
                
              </div-->
            <ul class="list-group">

                {{#actions}}
                <li class="list-group-item"><tt style="color:gray;">{{date}} </tt> {{{text}}}</li>
                {{/actions}}
            </ul>
        </div>
        {{/cards}}
        <hr><br><br>
        {{/lists}}
    </script>




    <script src="http://netdna.bootstrapcdn.com/bootstrap/3.0.3/js/bootstrap.min.js"></script>
    <script src="http://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js" type="text/javascript"></script>
    <script src="http://cdnjs.cloudflare.com/ajax/libs/mustache.js/0.7.2/mustache.min.js" type="text/javascript">
    </script>
    <script src="http://cdnjs.cloudflare.com/ajax/libs/moment.js/2.5.1/moment.min.js" type="text/javascript"></script>
    <script src="http://cdnjs.cloudflare.com/ajax/libs/marked/0.3.0/marked.min.js
" type="text/javascript"></script>
    <script type="text/javascript">
        function eatData( trelloJson ) {
            var data = {
                board: trelloJson.name,
                lists: [],
                ref: {}
            }

            for ( i in trelloJson.lists ) {
                var list = trelloJson.lists[ i ]
                if ( list.closed ) {
                    //continue
                }
                data.ref[ list.id ] = {
                    name: list.name,
                    cards: []
                }
                data.lists.push( data.ref[ list.id ] )
            }


            for ( i in trelloJson.cards ) {
                var card = trelloJson.cards[ i ]
                if ( card.closed ) {
                    //continue
                }

                data.ref[ card.id ] = {
                    name: card.name,
                    desc: marked( card.desc ),
                    actions: []
                }

                data.ref[ card.idList ].cards.push( data.ref[ card.id ] )

            }

            for ( i in trelloJson.actions ) {
                var action = trelloJson.actions[ i ]
                if ( action.type != "commentCard" ) {
                    continue
                }


                data.ref[ action.id ] = {
                    text: marked( action.data.text ),
                    date: moment( action.date ).format( 'YYYY-MM-DD' )
                }
                try {
                    data.ref[ action.data.card.id ].actions.push( data.ref[ action.id ] )
                } catch ( e ) {}
            }

            return data;
        }

        function showData( data ) {
            var template = $( '#template-output' ).html()
            console.log( JSON.stringify( data, null, 2 ) )
            $( '#out' ).html( Mustache.render( template, data ) )
        }

        function autorun() {
            if ( null == data ) {
                return alert( 'Please insert JSON data from Trello in the code' )
            }
            showData( eatData( data ) );
        }
        if ( document.addEventListener ) document.addEventListener( "DOMContentLoaded", autorun, false );
        else if ( document.attachEvent ) document.attachEvent( "onreadystatechange", autorun );
        else window.onload = autorun;


        data = null;
        
           data = {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "desc": "",
           "descData": null,
           "closed": false,
           "idOrganization": "6026193a66a9890a34067149",
           "shortLink": "xanN1duF",
           "powerUps": [],
           "dateLastActivity": "2021-02-12T06:09:46.506Z",
           "idTags": [],
           "datePluginDisable": null,
           "creationMethod": "automatic",
           "idBoardSource": null,
           "idMemberCreator": "6026192732328a14a53e94d8",
           "idEnterprise": null,
           "pinned": false,
           "starred": false,
           "url": "https://trello.com/b/xanN1duF/web-dev-hub-website",
           "shortUrl": "https://trello.com/b/xanN1duF",
           "ixUpdate": "30",
           "limits": {
           "attachments": {
           "perBoard": {
           "status": "ok",
           "disableAt": 36000,
           "warnAt": 32400
           },
           "perCard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "boards": {
           "totalMembersPerBoard": {
           "status": "ok",
           "disableAt": 1600,
           "warnAt": 1440
           }
           },
           "cards": {
           "openPerBoard": {
           "status": "ok",
           "disableAt": 5000,
           "warnAt": 4500
           },
           "openPerList": {
           "status": "ok",
           "disableAt": 5000,
           "warnAt": 4500
           },
           "totalPerBoard": {
           "status": "ok",
           "disableAt": 2000000,
           "warnAt": 1800000
           },
           "totalPerList": {
           "status": "ok",
           "disableAt": 1000000,
           "warnAt": 900000
           }
           },
           "checklists": {
           "perBoard": {
           "status": "ok",
           "disableAt": 2000000,
           "warnAt": 1800000
           },
           "perCard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           }
           },
           "checkItems": {
           "perChecklist": {
           "status": "ok",
           "disableAt": 200,
           "warnAt": 180
           }
           },
           "customFields": {
           "perBoard": {
           "status": "ok",
           "disableAt": 50,
           "warnAt": 45
           }
           },
           "customFieldOptions": {
           "perField": {
           "status": "ok",
           "disableAt": 50,
           "warnAt": 45
           }
           },
           "labels": {
           "perBoard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "lists": {
           "openPerBoard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           },
           "totalPerBoard": {
           "status": "ok",
           "disableAt": 3000,
           "warnAt": 2700
           }
           },
           "stickers": {
           "perCard": {
           "status": "ok",
           "disableAt": 70,
           "warnAt": 63
           }
           },
           "reactions": {
           "perAction": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           },
           "uniquePerAction": {
           "status": "ok",
           "disableAt": 17,
           "warnAt": 16
           }
           }
           },
           "enterpriseOwned": false,
           "subscribed": false,
           "templateGallery": null,
           "premiumFeatures": [],
           "dateLastView": "2021-02-12T06:10:06.275Z",
           "labelNames": {
           "green": "",
           "yellow": "",
           "orange": "",
           "red": "",
           "purple": "",
           "blue": "",
           "sky": "",
           "lime": "",
           "pink": "",
           "black": ""
           },
           "prefs": {
           "permissionLevel": "org",
           "hideVotes": false,
           "voting": "disabled",
           "comments": "members",
           "invitations": "members",
           "selfJoin": true,
           "cardCovers": true,
           "isTemplate": false,
           "cardAging": "regular",
           "calendarFeedEnabled": false,
           "background": "602606032e380738004a96bb",
           "backgroundImage":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/original/34e8349439184644f6bf4940a8ea606a/photo-1611955917566-70d110dc19f3",
           "backgroundImageScaled": [ {
           "width": 140,
           "height": 93,
           "url":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/140x93/15f103d54c224d53d69a4470cfcbe9ef/photo-1611955917566-70d110dc19f3.jpg"
           }, {
           "width": 256,
           "height": 171,
           "url":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/256x171/15f103d54c224d53d69a4470cfcbe9ef/photo-1611955917566-70d110dc19f3.jpg"
           }, {
           "width": 480,
           "height": 320,
           "url":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/480x320/15f103d54c224d53d69a4470cfcbe9ef/photo-1611955917566-70d110dc19f3.jpg"
           }, {
           "width": 960,
           "height": 640,
           "url":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/960x640/15f103d54c224d53d69a4470cfcbe9ef/photo-1611955917566-70d110dc19f3.jpg"
           }, {
           "width": 1024,
           "height": 683,
           "url":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/1024x683/15f103d54c224d53d69a4470cfcbe9ef/photo-1611955917566-70d110dc19f3.jpg"
           }, {
           "width": 2048,
           "height": 1366,
           "url":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/2048x1366/15f103d54c224d53d69a4470cfcbe9ef/photo-1611955917566-70d110dc19f3.jpg"
           }, {
           "width": 1280,
           "height": 854,
           "url":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/1280x854/15f103d54c224d53d69a4470cfcbe9ef/photo-1611955917566-70d110dc19f3.jpg"
           }, {
           "width": 1920,
           "height": 1280,
           "url":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/1920x1280/15f103d54c224d53d69a4470cfcbe9ef/photo-1611955917566-70d110dc19f3.jpg"
           }, {
           "width": 2400,
           "height": 1600,
           "url":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/2400x1600/15f103d54c224d53d69a4470cfcbe9ef/photo-1611955917566-70d110dc19f3.jpg"
           }, {
           "width": 2560,
           "height": 1707,
           "url":
           "https://trello-backgrounds.s3.amazonaws.com/SharedBackground/original/34e8349439184644f6bf4940a8ea606a/photo-1611955917566-70d110dc19f3"
           } ],
           "backgroundTile": false,
           "backgroundBrightness": "dark",
           "backgroundBottomColor": "#222222",
           "backgroundTopColor": "#363636",
           "canBePublic": true,
           "canBeEnterprise": true,
           "canBeOrg": true,
           "canBePrivate": true,
           "canInvite": true
           },
           "actions": [ {
           "id": "60261baac6f0794629a131ad",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "card": {
           "id": "60261baac6f0794629a131ac",
           "name": "Start implementing reusable react components",
           "idShort": 9,
           "shortLink": "ZeQlTEfp"
           },
           "list": {
           "id": "602619ce28343d8b99cab23c",
           "name": "To Do"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "createCard",
           "date": "2021-02-12T06:09:46.528Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261b97d363b10c50ce6f56",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "card": {
           "id": "60261b97d363b10c50ce6f55",
           "name": "Consolidate site building resources and remove unused code",
           "idShort": 8,
           "shortLink": "3omT4w2E"
           },
           "list": {
           "id": "602619ce28343d8b99cab23c",
           "name": "To Do"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "createCard",
           "date": "2021-02-12T06:09:27.273Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261b4c8afd7b371b96a47b",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "old": {
           "prefs": {
           "background": "602606b4f59f6b4c89a95cec"
           }
           },
           "board": {
           "prefs": {
           "background": "602606032e380738004a96bb"
           },
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "updateBoard",
           "date": "2021-02-12T06:08:12.451Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261b49f52d0188fbebeabc",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "old": {
           "prefs": {
           "background": "6026052da3595c7055b1a844"
           }
           },
           "board": {
           "prefs": {
           "background": "602606b4f59f6b4c89a95cec"
           },
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "updateBoard",
           "date": "2021-02-12T06:08:09.743Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261a91ae38502031702550",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "card": {
           "id": "60261a91ae3850203170254f",
           "name": "Unify Theme across pages",
           "idShort": 7,
           "shortLink": "ihBtbXPo"
           },
           "list": {
           "id": "602619ce28343d8b99cab23c",
           "name": "To Do"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "createCard",
           "date": "2021-02-12T06:05:05.715Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261a87bb51c819d6e95320",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "card": {
           "id": "60261a87bb51c819d6e9531f",
           "name": "Use the watch page from the work you did on mihir's website to add to your portfolio section",
           "idShort": 6,
           "shortLink": "LYRzJGCi"
           },
           "list": {
           "id": "602619ce28343d8b99cab23c",
           "name": "To Do"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "createCard",
           "date": "2021-02-12T06:04:55.980Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261a5f65476e111782617c",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "card": {
           "id": "60261a5f65476e111782617b",
           "name": "Organize Blog",
           "idShort": 5,
           "shortLink": "AteKMLQf"
           },
           "list": {
           "id": "602619ce28343d8b99cab23c",
           "name": "To Do"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "createCard",
           "date": "2021-02-12T06:04:15.467Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261a5a3266381e8182cec0",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "card": {
           "id": "60261a5a3266381e8182cebf",
           "name": "Add Fiddle Code Spaces wherever there are examples",
           "idShort": 4,
           "shortLink": "y5y8RtbH"
           },
           "list": {
           "id": "602619ce28343d8b99cab23c",
           "name": "To Do"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "createCard",
           "date": "2021-02-12T06:04:10.863Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261a45183c8c14ce192f22",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "card": {
           "id": "60261a45183c8c14ce192f21",
           "name": "Reorganize file structure to reduce redundancy",
           "idShort": 3,
           "shortLink": "kvSMfztl"
           },
           "list": {
           "id": "602619ce28343d8b99cab23c",
           "name": "To Do"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "createCard",
           "date": "2021-02-12T06:03:49.378Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261a2e215d2086ff273533",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "card": {
           "id": "60261a2e215d2086ff273532",
           "name": "Created Navigation Interface",
           "idShort": 2,
           "shortLink": "jciAoplj"
           },
           "list": {
           "id": "602619ce28343d8b99cab23d",
           "name": "Complete"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "createCard",
           "date": "2021-02-12T06:03:26.715Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261a24faad3a0435e90155",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "card": {
           "id": "60261a24faad3a0435e90154",
           "name": "Fixed sandbox text editor",
           "idShort": 1,
           "shortLink": "mjDuZvcp"
           },
           "list": {
           "id": "602619ce28343d8b99cab23d",
           "name": "Complete"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "createCard",
           "date": "2021-02-12T06:03:16.750Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "60261a013f423554c3584039",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "old": {
           "name": "Done"
           },
           "list": {
           "name": "Feature List",
           "id": "602619ce28343d8b99cab23e"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "updateList",
           "date": "2021-02-12T06:02:41.095Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "602619f89221c88712645c96",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "old": {
           "name": "Doing"
           },
           "list": {
           "name": "Complete",
           "id": "602619ce28343d8b99cab23d"
           },
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "updateList",
           "date": "2021-02-12T06:02:32.607Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "602619ce28343d8b99cab242",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           },
           "organization": {
           "id": "6026193a66a9890a34067149",
           "name": "web-dev-hub"
           }
           },
           "type": "addToOrganizationBoard",
           "date": "2021-02-12T06:01:50.125Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           }, {
           "id": "602619ce28343d8b99cab240",
           "idMemberCreator": "6026192732328a14a53e94d8",
           "data": {
           "creationMethod": "automatic",
           "board": {
           "id": "602619ce28343d8b99cab23b",
           "name": "web-dev-hub-website",
           "shortLink": "xanN1duF"
           }
           },
           "type": "createBoard",
           "date": "2021-02-12T06:01:50.121Z",
           "appCreator": null,
           "limits": {},
           "memberCreator": {
           "id": "6026192732328a14a53e94d8",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idMemberReferrer": null,
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true
           }
           } ],
           "cards": [ {
           "id": "60261a45183c8c14ce192f21",
           "address": null,
           "checkItemStates": null,
           "closed": false,
           "coordinates": null,
           "creationMethod": null,
           "dateLastActivity": "2021-02-12T06:03:49.356Z",
           "desc": "",
           "descData": null,
           "dueReminder": null,
           "idBoard": "602619ce28343d8b99cab23b",
           "idLabels": [],
           "idList": "602619ce28343d8b99cab23c",
           "idMembersVoted": [],
           "idShort": 3,
           "idAttachmentCover": null,
           "locationName": null,
           "manualCoverAttachment": false,
           "name": "Reorganize file structure to reduce redundancy",
           "pos": 65535,
           "shortLink": "kvSMfztl",
           "isTemplate": false,
           "cardRole": null,
           "badges": {
           "attachmentsByType": {
           "trello": {
           "board": 0,
           "card": 0
           }
           },
           "location": false,
           "votes": 0,
           "viewingMemberVoted": false,
           "subscribed": false,
           "fogbugz": "",
           "checkItems": 0,
           "checkItemsChecked": 0,
           "checkItemsEarliestDue": null,
           "comments": 0,
           "attachments": 0,
           "description": false,
           "due": null,
           "dueComplete": false,
           "start": null
           },
           "dueComplete": false,
           "due": null,
           "email": "bryancguner+2vuwbabqgeh2088w7a0+2vuwc58r276l56b9mw1+2jnb5wft3n@boards.trello.com",
           "idChecklists": [],
           "idMembers": [],
           "labels": [],
           "limits": {
           "attachments": {
           "perCard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "checklists": {
           "perCard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           }
           },
           "stickers": {
           "perCard": {
           "status": "ok",
           "disableAt": 70,
           "warnAt": 63
           }
           }
           },
           "shortUrl": "https://trello.com/c/kvSMfztl",
           "start": null,
           "subscribed": false,
           "url": "https://trello.com/c/kvSMfztl/3-reorganize-file-structure-to-reduce-redundancy",
           "cover": {
           "idAttachment": null,
           "color": null,
           "idUploadedBackground": null,
           "size": "normal",
           "brightness": "light",
           "idPlugin": null
           },
           "attachments": [],
           "pluginData": [],
           "customFieldItems": []
           }, {
           "id": "60261a5a3266381e8182cebf",
           "address": null,
           "checkItemStates": null,
           "closed": false,
           "coordinates": null,
           "creationMethod": null,
           "dateLastActivity": "2021-02-12T06:04:10.836Z",
           "desc": "",
           "descData": null,
           "dueReminder": null,
           "idBoard": "602619ce28343d8b99cab23b",
           "idLabels": [],
           "idList": "602619ce28343d8b99cab23c",
           "idMembersVoted": [],
           "idShort": 4,
           "idAttachmentCover": null,
           "locationName": null,
           "manualCoverAttachment": false,
           "name": "Add Fiddle Code Spaces wherever there are examples",
           "pos": 131071,
           "shortLink": "y5y8RtbH",
           "isTemplate": false,
           "cardRole": null,
           "badges": {
           "attachmentsByType": {
           "trello": {
           "board": 0,
           "card": 0
           }
           },
           "location": false,
           "votes": 0,
           "viewingMemberVoted": false,
           "subscribed": false,
           "fogbugz": "",
           "checkItems": 0,
           "checkItemsChecked": 0,
           "checkItemsEarliestDue": null,
           "comments": 0,
           "attachments": 0,
           "description": false,
           "due": null,
           "dueComplete": false,
           "start": null
           },
           "dueComplete": false,
           "due": null,
           "email": "bryancguner+2vuwbabqgeh2088w7a0+2vuwc7iwj0hfho7zf7j+0kk67x8d8y@boards.trello.com",
           "idChecklists": [],
           "idMembers": [],
           "labels": [],
           "limits": {
           "attachments": {
           "perCard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "checklists": {
           "perCard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           }
           },
           "stickers": {
           "perCard": {
           "status": "ok",
           "disableAt": 70,
           "warnAt": 63
           }
           }
           },
           "shortUrl": "https://trello.com/c/y5y8RtbH",
           "start": null,
           "subscribed": false,
           "url": "https://trello.com/c/y5y8RtbH/4-add-fiddle-code-spaces-wherever-there-are-examples",
           "cover": {
           "idAttachment": null,
           "color": null,
           "idUploadedBackground": null,
           "size": "normal",
           "brightness": "light",
           "idPlugin": null
           },
           "attachments": [],
           "pluginData": [],
           "customFieldItems": []
           }, {
           "id": "60261a5f65476e111782617b",
           "address": null,
           "checkItemStates": null,
           "closed": false,
           "coordinates": null,
           "creationMethod": null,
           "dateLastActivity": "2021-02-12T06:04:15.446Z",
           "desc": "",
           "descData": null,
           "dueReminder": null,
           "idBoard": "602619ce28343d8b99cab23b",
           "idLabels": [],
           "idList": "602619ce28343d8b99cab23c",
           "idMembersVoted": [],
           "idShort": 5,
           "idAttachmentCover": null,
           "locationName": null,
           "manualCoverAttachment": false,
           "name": "Organize Blog",
           "pos": 196607,
           "shortLink": "AteKMLQf",
           "isTemplate": false,
           "cardRole": null,
           "badges": {
           "attachmentsByType": {
           "trello": {
           "board": 0,
           "card": 0
           }
           },
           "location": false,
           "votes": 0,
           "viewingMemberVoted": false,
           "subscribed": false,
           "fogbugz": "",
           "checkItems": 0,
           "checkItemsChecked": 0,
           "checkItemsEarliestDue": null,
           "comments": 0,
           "attachments": 0,
           "description": false,
           "due": null,
           "dueComplete": false,
           "start": null
           },
           "dueComplete": false,
           "due": null,
           "email": "bryancguner+2vuwbabqgeh2088w7a0+2vuwc8354q752tm7urf+0qqpqysmvt@boards.trello.com",
           "idChecklists": [],
           "idMembers": [],
           "labels": [],
           "limits": {
           "attachments": {
           "perCard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "checklists": {
           "perCard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           }
           },
           "stickers": {
           "perCard": {
           "status": "ok",
           "disableAt": 70,
           "warnAt": 63
           }
           }
           },
           "shortUrl": "https://trello.com/c/AteKMLQf",
           "start": null,
           "subscribed": false,
           "url": "https://trello.com/c/AteKMLQf/5-organize-blog",
           "cover": {
           "idAttachment": null,
           "color": null,
           "idUploadedBackground": null,
           "size": "normal",
           "brightness": "light",
           "idPlugin": null
           },
           "attachments": [],
           "pluginData": [],
           "customFieldItems": []
           }, {
           "id": "60261a87bb51c819d6e9531f",
           "address": null,
           "checkItemStates": null,
           "closed": false,
           "coordinates": null,
           "creationMethod": null,
           "dateLastActivity": "2021-02-12T06:04:55.959Z",
           "desc": "",
           "descData": null,
           "dueReminder": null,
           "idBoard": "602619ce28343d8b99cab23b",
           "idLabels": [],
           "idList": "602619ce28343d8b99cab23c",
           "idMembersVoted": [],
           "idShort": 6,
           "idAttachmentCover": null,
           "locationName": null,
           "manualCoverAttachment": false,
           "name": "Use the watch page from the work you did on mihir's website to add to your portfolio section",
           "pos": 262143,
           "shortLink": "LYRzJGCi",
           "isTemplate": false,
           "cardRole": null,
           "badges": {
           "attachmentsByType": {
           "trello": {
           "board": 0,
           "card": 0
           }
           },
           "location": false,
           "votes": 0,
           "viewingMemberVoted": false,
           "subscribed": false,
           "fogbugz": "",
           "checkItems": 0,
           "checkItemsChecked": 0,
           "checkItemsEarliestDue": null,
           "comments": 0,
           "attachments": 0,
           "description": false,
           "due": null,
           "dueComplete": false,
           "start": null
           },
           "dueComplete": false,
           "due": null,
           "email": "bryancguner+2vuwbabqgeh2088w7a0+2vuwccg681pos2ess2n+1g6ybiufvi@boards.trello.com",
           "idChecklists": [],
           "idMembers": [],
           "labels": [],
           "limits": {
           "attachments": {
           "perCard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "checklists": {
           "perCard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           }
           },
           "stickers": {
           "perCard": {
           "status": "ok",
           "disableAt": 70,
           "warnAt": 63
           }
           }
           },
           "shortUrl": "https://trello.com/c/LYRzJGCi",
           "start": null,
           "subscribed": false,
           "url":
           "https://trello.com/c/LYRzJGCi/6-use-the-watch-page-from-the-work-you-did-on-mihirs-website-to-add-to-your-portfolio-section",
           "cover": {
           "idAttachment": null,
           "color": null,
           "idUploadedBackground": null,
           "size": "normal",
           "brightness": "light",
           "idPlugin": null
           },
           "attachments": [],
           "pluginData": [],
           "customFieldItems": []
           }, {
           "id": "60261a91ae3850203170254f",
           "address": null,
           "checkItemStates": null,
           "closed": false,
           "coordinates": null,
           "creationMethod": null,
           "dateLastActivity": "2021-02-12T06:05:05.694Z",
           "desc": "",
           "descData": null,
           "dueReminder": null,
           "idBoard": "602619ce28343d8b99cab23b",
           "idLabels": [],
           "idList": "602619ce28343d8b99cab23c",
           "idMembersVoted": [],
           "idShort": 7,
           "idAttachmentCover": null,
           "locationName": null,
           "manualCoverAttachment": false,
           "name": "Unify Theme across pages",
           "pos": 327679,
           "shortLink": "ihBtbXPo",
           "isTemplate": false,
           "cardRole": null,
           "badges": {
           "attachmentsByType": {
           "trello": {
           "board": 0,
           "card": 0
           }
           },
           "location": false,
           "votes": 0,
           "viewingMemberVoted": false,
           "subscribed": false,
           "fogbugz": "",
           "checkItems": 0,
           "checkItemsChecked": 0,
           "checkItemsEarliestDue": null,
           "comments": 0,
           "attachments": 0,
           "description": false,
           "due": null,
           "dueComplete": false,
           "start": null
           },
           "dueComplete": false,
           "due": null,
           "email": "bryancguner+2vuwbabqgeh2088w7a0+2vuwcdiwjrt5fjardxr+1lb64pajid@boards.trello.com",
           "idChecklists": [],
           "idMembers": [],
           "labels": [],
           "limits": {
           "attachments": {
           "perCard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "checklists": {
           "perCard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           }
           },
           "stickers": {
           "perCard": {
           "status": "ok",
           "disableAt": 70,
           "warnAt": 63
           }
           }
           },
           "shortUrl": "https://trello.com/c/ihBtbXPo",
           "start": null,
           "subscribed": false,
           "url": "https://trello.com/c/ihBtbXPo/7-unify-theme-across-pages",
           "cover": {
           "idAttachment": null,
           "color": null,
           "idUploadedBackground": null,
           "size": "normal",
           "brightness": "light",
           "idPlugin": null
           },
           "attachments": [],
           "pluginData": [],
           "customFieldItems": []
           }, {
           "id": "60261b97d363b10c50ce6f55",
           "address": null,
           "checkItemStates": null,
           "closed": false,
           "coordinates": null,
           "creationMethod": null,
           "dateLastActivity": "2021-02-12T06:09:27.246Z",
           "desc": "",
           "descData": null,
           "dueReminder": null,
           "idBoard": "602619ce28343d8b99cab23b",
           "idLabels": [],
           "idList": "602619ce28343d8b99cab23c",
           "idMembersVoted": [],
           "idShort": 8,
           "idAttachmentCover": null,
           "locationName": null,
           "manualCoverAttachment": false,
           "name": "Consolidate site building resources and remove unused code",
           "pos": 393215,
           "shortLink": "3omT4w2E",
           "isTemplate": false,
           "cardRole": null,
           "badges": {
           "attachmentsByType": {
           "trello": {
           "board": 0,
           "card": 0
           }
           },
           "location": false,
           "votes": 0,
           "viewingMemberVoted": false,
           "subscribed": false,
           "fogbugz": "",
           "checkItems": 0,
           "checkItemsChecked": 0,
           "checkItemsEarliestDue": null,
           "comments": 0,
           "attachments": 0,
           "description": false,
           "due": null,
           "dueComplete": false,
           "start": null
           },
           "dueComplete": false,
           "due": null,
           "email": "bryancguner+2vuwbabqgeh2088w7a0+2vuwd5vg4fbi41ocklx+0agjezcvrz@boards.trello.com",
           "idChecklists": [],
           "idMembers": [],
           "labels": [],
           "limits": {
           "attachments": {
           "perCard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "checklists": {
           "perCard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           }
           },
           "stickers": {
           "perCard": {
           "status": "ok",
           "disableAt": 70,
           "warnAt": 63
           }
           }
           },
           "shortUrl": "https://trello.com/c/3omT4w2E",
           "start": null,
           "subscribed": false,
           "url": "https://trello.com/c/3omT4w2E/8-consolidate-site-building-resources-and-remove-unused-code",
           "cover": {
           "idAttachment": null,
           "color": null,
           "idUploadedBackground": null,
           "size": "normal",
           "brightness": "light",
           "idPlugin": null
           },
           "attachments": [],
           "pluginData": [],
           "customFieldItems": []
           }, {
           "id": "60261baac6f0794629a131ac",
           "address": null,
           "checkItemStates": null,
           "closed": false,
           "coordinates": null,
           "creationMethod": null,
           "dateLastActivity": "2021-02-12T06:09:46.506Z",
           "desc": "",
           "descData": null,
           "dueReminder": null,
           "idBoard": "602619ce28343d8b99cab23b",
           "idLabels": [],
           "idList": "602619ce28343d8b99cab23c",
           "idMembersVoted": [],
           "idShort": 9,
           "idAttachmentCover": null,
           "locationName": null,
           "manualCoverAttachment": false,
           "name": "Start implementing reusable react components",
           "pos": 458751,
           "shortLink": "ZeQlTEfp",
           "isTemplate": false,
           "cardRole": null,
           "badges": {
           "attachmentsByType": {
           "trello": {
           "board": 0,
           "card": 0
           }
           },
           "location": false,
           "votes": 0,
           "viewingMemberVoted": false,
           "subscribed": false,
           "fogbugz": "",
           "checkItems": 0,
           "checkItemsChecked": 0,
           "checkItemsEarliestDue": null,
           "comments": 0,
           "attachments": 0,
           "description": false,
           "due": null,
           "dueComplete": false,
           "start": null
           },
           "dueComplete": false,
           "due": null,
           "email": "bryancguner+2vuwbabqgeh2088w7a0+2vuwd7x85gfttl7incc+2epb2srcci@boards.trello.com",
           "idChecklists": [],
           "idMembers": [],
           "labels": [],
           "limits": {
           "attachments": {
           "perCard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "checklists": {
           "perCard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           }
           },
           "stickers": {
           "perCard": {
           "status": "ok",
           "disableAt": 70,
           "warnAt": 63
           }
           }
           },
           "shortUrl": "https://trello.com/c/ZeQlTEfp",
           "start": null,
           "subscribed": false,
           "url": "https://trello.com/c/ZeQlTEfp/9-start-implementing-reusable-react-components",
           "cover": {
           "idAttachment": null,
           "color": null,
           "idUploadedBackground": null,
           "size": "normal",
           "brightness": "light",
           "idPlugin": null
           },
           "attachments": [],
           "pluginData": [],
           "customFieldItems": []
           }, {
           "id": "60261a24faad3a0435e90154",
           "address": null,
           "checkItemStates": null,
           "closed": false,
           "coordinates": null,
           "creationMethod": null,
           "dateLastActivity": "2021-02-12T06:03:16.725Z",
           "desc": "",
           "descData": null,
           "dueReminder": null,
           "idBoard": "602619ce28343d8b99cab23b",
           "idLabels": [],
           "idList": "602619ce28343d8b99cab23d",
           "idMembersVoted": [],
           "idShort": 1,
           "idAttachmentCover": null,
           "locationName": null,
           "manualCoverAttachment": false,
           "name": "Fixed sandbox text editor",
           "pos": 65535,
           "shortLink": "mjDuZvcp",
           "isTemplate": false,
           "cardRole": null,
           "badges": {
           "attachmentsByType": {
           "trello": {
           "board": 0,
           "card": 0
           }
           },
           "location": false,
           "votes": 0,
           "viewingMemberVoted": false,
           "subscribed": false,
           "fogbugz": "",
           "checkItems": 0,
           "checkItemsChecked": 0,
           "checkItemsEarliestDue": null,
           "comments": 0,
           "attachments": 0,
           "description": false,
           "due": null,
           "dueComplete": false,
           "start": null
           },
           "dueComplete": false,
           "due": null,
           "email": "bryancguner+2vuwbabqgeh2088w7a0+2vuwc1rq35bmkagkrpw+1s0s59ba8r@boards.trello.com",
           "idChecklists": [],
           "idMembers": [],
           "labels": [],
           "limits": {
           "attachments": {
           "perCard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "checklists": {
           "perCard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           }
           },
           "stickers": {
           "perCard": {
           "status": "ok",
           "disableAt": 70,
           "warnAt": 63
           }
           }
           },
           "shortUrl": "https://trello.com/c/mjDuZvcp",
           "start": null,
           "subscribed": false,
           "url": "https://trello.com/c/mjDuZvcp/1-fixed-sandbox-text-editor",
           "cover": {
           "idAttachment": null,
           "color": null,
           "idUploadedBackground": null,
           "size": "normal",
           "brightness": "light",
           "idPlugin": null
           },
           "attachments": [],
           "pluginData": [],
           "customFieldItems": []
           }, {
           "id": "60261a2e215d2086ff273532",
           "address": null,
           "checkItemStates": null,
           "closed": false,
           "coordinates": null,
           "creationMethod": null,
           "dateLastActivity": "2021-02-12T06:03:26.695Z",
           "desc": "",
           "descData": null,
           "dueReminder": null,
           "idBoard": "602619ce28343d8b99cab23b",
           "idLabels": [],
           "idList": "602619ce28343d8b99cab23d",
           "idMembersVoted": [],
           "idShort": 2,
           "idAttachmentCover": null,
           "locationName": null,
           "manualCoverAttachment": false,
           "name": "Created Navigation Interface",
           "pos": 131071,
           "shortLink": "jciAoplj",
           "isTemplate": false,
           "cardRole": null,
           "badges": {
           "attachmentsByType": {
           "trello": {
           "board": 0,
           "card": 0
           }
           },
           "location": false,
           "votes": 0,
           "viewingMemberVoted": false,
           "subscribed": false,
           "fogbugz": "",
           "checkItems": 0,
           "checkItemsChecked": 0,
           "checkItemsEarliestDue": null,
           "comments": 0,
           "attachments": 0,
           "description": false,
           "due": null,
           "dueComplete": false,
           "start": null
           },
           "dueComplete": false,
           "due": null,
           "email": "bryancguner+2vuwbabqgeh2088w7a0+2vuwc2rcm4e4a9muvjm+1oy3nx7p2q@boards.trello.com",
           "idChecklists": [],
           "idMembers": [],
           "labels": [],
           "limits": {
           "attachments": {
           "perCard": {
           "status": "ok",
           "disableAt": 1000,
           "warnAt": 900
           }
           },
           "checklists": {
           "perCard": {
           "status": "ok",
           "disableAt": 500,
           "warnAt": 450
           }
           },
           "stickers": {
           "perCard": {
           "status": "ok",
           "disableAt": 70,
           "warnAt": 63
           }
           }
           },
           "shortUrl": "https://trello.com/c/jciAoplj",
           "start": null,
           "subscribed": false,
           "url": "https://trello.com/c/jciAoplj/2-created-navigation-interface",
           "cover": {
           "idAttachment": null,
           "color": null,
           "idUploadedBackground": null,
           "size": "normal",
           "brightness": "light",
           "idPlugin": null
           },
           "attachments": [],
           "pluginData": [],
           "customFieldItems": []
           } ],
           "labels": [ {
           "id": "602619ce86c6bc9cc5bc0a49",
           "idBoard": "602619ce28343d8b99cab23b",
           "name": "",
           "color": "green"
           }, {
           "id": "602619ce86c6bc9cc5bc0a4b",
           "idBoard": "602619ce28343d8b99cab23b",
           "name": "",
           "color": "yellow"
           }, {
           "id": "602619ce86c6bc9cc5bc0a4d",
           "idBoard": "602619ce28343d8b99cab23b",
           "name": "",
           "color": "orange"
           }, {
           "id": "602619ce86c6bc9cc5bc0a4f",
           "idBoard": "602619ce28343d8b99cab23b",
           "name": "",
           "color": "purple"
           }, {
           "id": "602619ce86c6bc9cc5bc0a52",
           "idBoard": "602619ce28343d8b99cab23b",
           "name": "",
           "color": "blue"
           }, {
           "id": "602619ce86c6bc9cc5bc0a53",
           "idBoard": "602619ce28343d8b99cab23b",
           "name": "",
           "color": "red"
           } ],
           "lists": [ {
           "id": "602619ce28343d8b99cab23c",
           "name": "To Do",
           "closed": false,
           "pos": 16384,
           "softLimit": null,
           "creationMethod": "automatic",
           "idBoard": "602619ce28343d8b99cab23b",
           "limits": {
           "cards": {
           "openPerList": {
           "status": "ok",
           "disableAt": 5000,
           "warnAt": 4500
           },
           "totalPerList": {
           "status": "ok",
           "disableAt": 1000000,
           "warnAt": 900000
           }
           }
           },
           "subscribed": false
           }, {
           "id": "602619ce28343d8b99cab23d",
           "name": "Complete",
           "closed": false,
           "pos": 32768,
           "softLimit": null,
           "creationMethod": "automatic",
           "idBoard": "602619ce28343d8b99cab23b",
           "limits": {
           "cards": {
           "openPerList": {
           "status": "ok",
           "disableAt": 5000,
           "warnAt": 4500
           },
           "totalPerList": {
           "status": "ok",
           "disableAt": 1000000,
           "warnAt": 900000
           }
           }
           },
           "subscribed": false
           }, {
           "id": "602619ce28343d8b99cab23e",
           "name": "Feature List",
           "closed": false,
           "pos": 49152,
           "softLimit": null,
           "creationMethod": "automatic",
           "idBoard": "602619ce28343d8b99cab23b",
           "limits": {
           "cards": {
           "openPerList": {
           "status": "ok",
           "disableAt": 5000,
           "warnAt": 4500
           },
           "totalPerList": {
           "status": "ok",
           "disableAt": 1000000,
           "warnAt": 900000
           }
           }
           },
           "subscribed": false
           } ],
           "members": [ {
           "id": "6026192732328a14a53e94d8",
           "bio": "",
           "bioData": null,
           "confirmed": true,
           "memberType": "normal",
           "username": "bryancguner",
           "activityBlocked": false,
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "fullName": "Bryan C Guner",
           "idEnterprise": null,
           "idEnterprisesDeactivated": [],
           "idMemberReferrer": null,
           "idPremOrgsAdmin": [],
           "initials": "BG",
           "nonPublic": {
           "fullName": "Bryan Guner",
           "initials": "BG",
           "avatarUrl":
           "https://trello-members.s3.amazonaws.com/6026192732328a14a53e94d8/bbd362d2e6a84e455c89025c83f5edda",
           "avatarHash": "bbd362d2e6a84e455c89025c83f5edda"
           },
           "nonPublicAvailable": true,
           "products": [],
           "url": "https://trello.com/bryancguner",
           "status": "disconnected"
           } ],
           "checklists": [],
           "customFields": [],
           "memberships": [ {
           "id": "602619ce28343d8b99cab23f",
           "idMember": "6026192732328a14a53e94d8",
           "memberType": "admin",
           "unconfirmed": false,
           "deactivated": false
           } ],
           "pluginData": []
           }

 
    </script>
</body>

</html>




```
