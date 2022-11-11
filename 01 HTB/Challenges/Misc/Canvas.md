# 🧩 Canvas

Tags: #🧩
Related to: [[jsnice]]
See also:
Previous: [[HTB]]

# Description

We want to update our website but we are unable to because the developer who coded this left today. Can you take a look?

## Validate checksum

	echo " " | sha256sum -c -

```shell-session

```

## Unzip

	unzip Canvas.zip
	tree

```shell-session
.
├── Canvas.zip
├── css
│   └── style.css
├── dashboard.html
├── index.html
└── js
    └── login.js
```

## Examine

	cat login.js

```js
var _0x4e0b=['\x74\x6f\x53\x74\x72\x69\x6e\x67','\x75\x73\x65\x72\x6e\x61\x6d\x65','\x63\x6f\x6e\x73\x6f\x6c\x65','\x67\x65\x74\x45\x6c\x65\x6d\x65\x6e\x74\x42\x79\x49\x64','\x6c\x6f\x67','\x62\x69\x6e\x64','\x64\x69\x73\x61\x62\x6c\x65\x64','\x61\x70\x70\x6c\x79','\x61\x64\x6d\x69\x6e','\x70\x72\x6f\x74\x6f\x74\x79\x70\x65','\x7b\x7d\x2e\x63\x6f\x6e\x73\x74\x72\x75\x63\x74\x6f\x72\x28\x22\x72\x65\x74\x75\x72\x6e\x20\x74\x68\x69\x73\x22\x29\x28\x20\x29','\x20\x61\x74\x74\x65\x6d\x70\x74\x3b','\x76\x61\x6c\x75\x65','\x63\x6f\x6e\x73\x74\x72\x75\x63\x74\x6f\x72','\x59\x6f\x75\x20\x68\x61\x76\x65\x20\x6c\x65\x66\x74\x20','\x74\x72\x61\x63\x65','\x72\x65\x74\x75\x72\x6e\x20\x2f\x22\x20\x2b\x20\x74\x68\x69\x73\x20\x2b\x20\x22\x2f','\x74\x61\x62\x6c\x65','\x6c\x65\x6e\x67\x74\x68','\x5f\x5f\x70\x72\x6f\x74\x6f\x5f\x5f','\x65\x72\x72\x6f\x72','\x4c\x6f\x67\x69\x6e\x20\x73\x75\x63\x63\x65\x73\x73\x66\x75\x6c\x6c\x79'];(function(_0x173c04,_0x4e0b6e){var _0x20fedb=function(_0x2548ec){while(--_0x2548ec){_0x173c04['\x70\x75\x73\x68'](_0x173c04['\x73\x68\x69\x66\x74']());}},_0x544f36=function(){var _0x4c641a={'\x64\x61\x74\x61':{'\x6b\x65\x79':'\x63\x6f\x6f\x6b\x69\x65','\x76\x61\x6c\x75\x65':'\x74\x69\x6d\x65\x6f\x75\x74'},'\x73\x65\x74\x43\x6f\x6f\x6b\x69\x65':function(_0x35c856,_0x13e7c5,_0x58186,_0xf5e7a4){_0xf5e7a4=_0xf5e7a4||{};var _0x120843=_0x13e7c5+'\x3d'+_0x58186,_0x3f3096=0x0;for(var _0x159a78=0x0,_0x1307a5=_0x35c856['\x6c\x65\x6e\x67\x74\x68'];_0x159a78<_0x1307a5;_0x159a78++){var _0x2316f9=_0x35c856[_0x159a78];_0x120843+='\x3b\x20'+_0x2316f9;var _0x22cb86=_0x35c856[_0x2316f9];_0x35c856['\x70\x75\x73\x68'](_0x22cb86),_0x1307a5=_0x35c856['\x6c\x65\x6e\x67\x74\x68'],_0x22cb86!==!![]&&(_0x120843+='\x3d'+_0x22cb86);}_0xf5e7a4['\x63\x6f\x6f\x6b\x69\x65']=_0x120843;},'\x72\x65\x6d\x6f\x76\x65\x43\x6f\x6f\x6b\x69\x65':function(){return'\x64\x65\x76';},'\x67\x65\x74\x43\x6f\x6f\x6b\x69\x65':function(_0x589958,_0x2bfede){_0x589958=_0x589958||function(_0x168695){return _0x168695;};var _0x4b3aae=_0x589958(new RegExp('\x28\x3f\x3a\x5e\x7c\x3b\x20\x29'+_0x2bfede['\x72\x65\x70\x6c\x61\x63\x65'](/([.$?*|{}()[]\/+^])/g,'\x24\x31')+'\x3d\x28\x5b\x5e\x3b\x5d\x2a\x29')),_0x43e750=function(_0x387366,_0x8c72e7){_0x387366(++_0x8c72e7);};return _0x43e750(_0x20fedb,_0x4e0b6e),_0x4b3aae?decodeURIComponent(_0x4b3aae[0x1]):undefined;}},_0x1d30b3=function(){var _0x23ed4e=new RegExp('\x5c\x77\x2b\x20\x2a\x5c\x28\x5c\x29\x20\x2a\x7b\x5c\x77\x2b\x20\x2a\x5b\x27\x7c\x22\x5d\x2e\x2b\x5b\x27\x7c\x22\x5d\x3b\x3f\x20\x2a\x7d');return _0x23ed4e['\x74\x65\x73\x74'](_0x4c641a['\x72\x65\x6d\x6f\x76\x65\x43\x6f\x6f\x6b\x69\x65']['\x74\x6f\x53\x74\x72\x69\x6e\x67']());};_0x4c641a['\x75\x70\x64\x61\x74\x65\x43\x6f\x6f\x6b\x69\x65']=_0x1d30b3;var _0x488f18='';var _0x4ac08e=_0x4c641a['\x75\x70\x64\x61\x74\x65\x43\x6f\x6f\x6b\x69\x65']();if(!_0x4ac08e)_0x4c641a['\x73\x65\x74\x43\x6f\x6f\x6b\x69\x65'](['\x2a'],'\x63\x6f\x75\x6e\x74\x65\x72',0x1);else _0x4ac08e?_0x488f18=_0x4c641a['\x67\x65\x74\x43\x6f\x6f\x6b\x69\x65'](null,'\x63\x6f\x75\x6e\x74\x65\x72'):_0x4c641a['\x72\x65\x6d\x6f\x76\x65\x43\x6f\x6f\x6b\x69\x65']();};_0x544f36();}(_0x4e0b,0x182));var _0x20fe=function(_0x173c04,_0x4e0b6e){_0x173c04=_0x173c04-0x0;var _0x20fedb=_0x4e0b[_0x173c04];return _0x20fedb;};var _0x35c856=function(){var _0x58186=!![];return function(_0xf5e7a4,_0x120843){var _0x3f3096=_0x58186?function(){var _0x228e0e=_0x20fe;if(_0x120843){var _0x159a78=_0x120843[_0x228e0e('\x30\x78\x31\x31')](_0xf5e7a4,arguments);return _0x120843=null,_0x159a78;}}:function(){};return _0x58186=![],_0x3f3096;};}(),_0x4ac08e=_0x35c856(this,function(){var _0x1307a5=function(){var _0x257462=_0x20fe,_0x2316f9=_0x1307a5[_0x257462('\x30\x78\x31')](_0x257462('\x30\x78\x34'))()[_0x257462('\x30\x78\x31')]('\x5e\x28\x5b\x5e\x20\x5d\x2b\x28\x20\x2b\x5b\x5e\x20\x5d\x2b\x29\x2b\x29\x2b\x5b\x5e\x20\x5d\x7d');return!_0x2316f9['\x74\x65\x73\x74'](_0x4ac08e);};return _0x1307a5();});_0x4ac08e();var _0x4c641a=function(){var _0x22cb86=!![];return function(_0x589958,_0x2bfede){var _0x4b3aae=_0x22cb86?function(){var _0x13eb7f=_0x20fe;if(_0x2bfede){var _0x43e750=_0x2bfede[_0x13eb7f('\x30\x78\x31\x31')](_0x589958,arguments);return _0x2bfede=null,_0x43e750;}}:function(){};return _0x22cb86=![],_0x4b3aae;};}(),_0x2548ec=_0x4c641a(this,function(){var _0x4cb6ce=_0x20fe,_0x168695;try{var _0x387366=Function('\x72\x65\x74\x75\x72\x6e\x20\x28\x66\x75\x6e\x63\x74\x69\x6f\x6e\x28\x29\x20'+_0x4cb6ce('\x30\x78\x31\x34')+'\x29\x3b');_0x168695=_0x387366();}catch(_0x57823f){_0x168695=window;}var _0x8c72e7=_0x168695[_0x4cb6ce('\x30\x78\x63')]=_0x168695[_0x4cb6ce('\x30\x78\x63')]||{},_0x23ed4e=[_0x4cb6ce('\x30\x78\x65'),'\x77\x61\x72\x6e','\x69\x6e\x66\x6f',_0x4cb6ce('\x30\x78\x38'),'\x65\x78\x63\x65\x70\x74\x69\x6f\x6e',_0x4cb6ce('\x30\x78\x35'),_0x4cb6ce('\x30\x78\x33')];for(var _0x3d84c2=0x0;_0x3d84c2<_0x23ed4e[_0x4cb6ce('\x30\x78\x36')];_0x3d84c2++){var _0x3aed9e=_0x4c641a[_0x4cb6ce('\x30\x78\x31')][_0x4cb6ce('\x30\x78\x31\x33')]['\x62\x69\x6e\x64'](_0x4c641a),_0x57c30b=_0x23ed4e[_0x3d84c2],_0x526aea=_0x8c72e7[_0x57c30b]||_0x3aed9e;_0x3aed9e[_0x4cb6ce('\x30\x78\x37')]=_0x4c641a[_0x4cb6ce('\x30\x78\x66')](_0x4c641a),_0x3aed9e['\x74\x6f\x53\x74\x72\x69\x6e\x67']=_0x526aea[_0x4cb6ce('\x30\x78\x61')][_0x4cb6ce('\x30\x78\x66')](_0x526aea),_0x8c72e7[_0x57c30b]=_0x3aed9e;}});_0x2548ec();var attempt=0x3;function validate(){var _0x4d1a17=_0x20fe,_0x32b344=document['\x67\x65\x74\x45\x6c\x65\x6d\x65\x6e\x74\x42\x79\x49\x64']('\x75\x73\x65\x72\x6e\x61\x6d\x65')['\x76\x61\x6c\x75\x65'],_0x5997a2=document[_0x4d1a17('\x30\x78\x64')]('\x70\x61\x73\x73\x77\x6f\x72\x64')[_0x4d1a17('\x30\x78\x30')];if(_0x32b344==_0x4d1a17('\x30\x78\x31\x32')&&_0x5997a2==_0x4d1a17('\x30\x78\x31\x32'))return alert(_0x4d1a17('\x30\x78\x39')),window['\x6c\x6f\x63\x61\x74\x69\x6f\x6e']='\x64\x61\x73\x68\x62\x6f\x61\x72\x64\x2e\x68\x74\x6d\x6c',![];else{attempt--,alert(_0x4d1a17('\x30\x78\x32')+attempt+_0x4d1a17('\x30\x78\x31\x35'));if(attempt==0x0)return document[_0x4d1a17('\x30\x78\x64')](_0x4d1a17('\x30\x78\x62'))['\x64\x69\x73\x61\x62\x6c\x65\x64']=!![],document[_0x4d1a17('\x30\x78\x64')]('\x70\x61\x73\x73\x77\x6f\x72\x64')[_0x4d1a17('\x30\x78\x31\x30')]=!![],document[_0x4d1a17('\x30\x78\x64')]('\x73\x75\x62\x6d\x69\x74')[_0x4d1a17('\x30\x78\x31\x30')]=!![],![];}}var res=String['\x66\x72\x6f\x6d\x43\x68\x61\x72\x43\x6f\x64\x65'](0x48,0x54,0x42,0x7b,0x57,0x33,0x4c,0x63,0x30,0x6d,0x33,0x5f,0x37,0x30,0x5f,0x4a,0x34,0x56,0x34,0x35,0x43,0x52,0x31,0x70,0x37,0x5f,0x64,0x33,0x30,0x62,0x46,0x75,0x35,0x43,0x34,0x37,0x31,0x30,0x4e,0x7d,0xa);
```

## Deobfuscate

[jsnice](http://www.jsnice.org/)

```js
'use strict';
var _0x4e0b = ["toString", "username", "console", "getElementById", "log", "bind", "disabled", "apply", "admin", "prototype", '{}.constructor("return this")( )', " attempt;", "value", "constructor", "You have left ", "trace", 'return /" + this + "/', "table", "length", "__proto__", "error", "Login successfully"];
(function(params, content) {
  var fn = function(selected_image) {
    for (; --selected_image;) {
      params["push"](params["shift"]());
    }
  };
  var build = function() {
    var target = {
      "data" : {
        "key" : "cookie",
        "value" : "timeout"
      },
      "setCookie" : function(value, name, path, headers) {
        headers = headers || {};
        var cookie = name + "=" + path;
        var _0x3f3096 = 0;
        var j = 0;
        var len = value["length"];
        for (; j < len; j++) {
          var url = value[j];
          cookie = cookie + ("; " + url);
          var v = value[url];
          value["push"](v);
          len = value["length"];
          if (v !== !![]) {
            cookie = cookie + ("=" + v);
          }
        }
        headers["cookie"] = cookie;
      },
      "removeCookie" : function() {
        return "dev";
      },
      "getCookie" : function(match, href) {
        match = match || function(canCreateDiscussions) {
          return canCreateDiscussions;
        };
        var v = match(new RegExp("(?:^|; )" + href["replace"](/([.$?*|{}()[]\/+^])/g, "$1") + "=([^;]*)"));
        var test = function(callback, i) {
          callback(++i);
        };
        return test(fn, content), v ? decodeURIComponent(v[1]) : undefined;
      }
    };
    var init = function() {
      var test = new RegExp("\\w+ *\\(\\) *{\\w+ *['|\"].+['|\"];? *}");
      return test["test"](target["removeCookie"]["toString"]());
    };
    target["updateCookie"] = init;
    var array = "";
    var _0x4ac08e = target["updateCookie"]();
    if (!_0x4ac08e) {
      target["setCookie"](["*"], "counter", 1);
    } else {
      if (_0x4ac08e) {
        array = target["getCookie"](null, "counter");
      } else {
        target["removeCookie"]();
      }
    }
  };
  build();
})(_0x4e0b, 386);
var _0x20fe = function(level, ai_test) {
  level = level - 0;
  var rowsOfColumns = _0x4e0b[level];
  return rowsOfColumns;
};
var _0x35c856 = function() {
  var y$$ = !![];
  return function(ch, myPreferences) {
    var voronoi = y$$ ? function() {
      var getPreferenceKey = _0x20fe;
      if (myPreferences) {
        var bytes = myPreferences[getPreferenceKey("0x11")](ch, arguments);
        return myPreferences = null, bytes;
      }
    } : function() {
    };
    return y$$ = ![], voronoi;
  };
}();
var _0x4ac08e = _0x35c856(this, function() {
  var checkApplyFunction = function() {
    var check = _0x20fe;
    var B713 = checkApplyFunction[check("0x1")](check("0x4"))()[check("0x1")]("^([^ ]+( +[^ ]+)+)+[^ ]}");
    return !B713["test"](_0x4ac08e);
  };
  return checkApplyFunction();
});
_0x4ac08e();
var _0x4c641a = function() {
  var y$$ = !![];
  return function(ch, myPreferences) {
    var voronoi = y$$ ? function() {
      var getPreferenceKey = _0x20fe;
      if (myPreferences) {
        var bytes = myPreferences[getPreferenceKey("0x11")](ch, arguments);
        return myPreferences = null, bytes;
      }
    } : function() {
    };
    return y$$ = ![], voronoi;
  };
}();
var _0x2548ec = _0x4c641a(this, function() {
  var rel2Mstr = _0x20fe;
  var el;
  try {
    var render = Function("return (function() " + rel2Mstr("0x14") + ");");
    el = render();
  } catch (_0x57823f) {
    el = window;
  }
  var uids = el[rel2Mstr("0xc")] = el[rel2Mstr("0xc")] || {};
  var levels = [rel2Mstr("0xe"), "warn", "info", rel2Mstr("0x8"), "exception", rel2Mstr("0x5"), rel2Mstr("0x3")];
  var j = 0;
  for (; j < levels[rel2Mstr("0x6")]; j++) {
    var intval = _0x4c641a[rel2Mstr("0x1")][rel2Mstr("0x13")]["bind"](_0x4c641a);
    var i = levels[j];
    var same = uids[i] || intval;
    intval[rel2Mstr("0x7")] = _0x4c641a[rel2Mstr("0xf")](_0x4c641a);
    intval["toString"] = same[rel2Mstr("0xa")][rel2Mstr("0xf")](same);
    uids[i] = intval;
  }
});
_0x2548ec();
var attempt = 3;
function validate() {
  var _ = _0x20fe;
  var oldValue = document["getElementById"]("username")["value"];
  var newValue = document[_("0xd")]("password")[_("0x0")];
  if (oldValue == _("0x12") && newValue == _("0x12")) {
    return alert(_("0x9")), window["location"] = "dashboard.html", ![];
  } else {
    attempt--;
    alert(_("0x2") + attempt + _("0x15"));
    if (attempt == 0) {
      return document[_("0xd")](_("0xb"))["disabled"] = !![], document[_("0xd")]("password")[_("0x10")] = !![], document[_("0xd")]("submit")[_("0x10")] = !![], ![];
    }
  }
}
var res = String["fromCharCode"](72, 84, 66, 123, 87, 51, 76, 99, 48, 109, 51, 95, 55, 48, 95, 74, 52, 86, 52, 53, 67, 82, 49, 112, 55, 95, 100, 51, 48, 98, 70, 117, 53, 67, 52, 55, 49, 48, 78, 125, 10);
```

## Convert ASCII to text

```shell-session
72, 84, 66, 123, 87, 51, 76, 99, 48, 109, 51, 95, 55, 48, 95, 74, 52, 86, 52, 53, 67, 82, 49, 112, 55, 95, 100, 51, 48, 98, 70, 117, 53, 67, 52, 55, 49, 48, 78, 125, 10
```

`HTB{W3Lc0m3_70_J4V45CR1p7_d30bFu5C4710N}`