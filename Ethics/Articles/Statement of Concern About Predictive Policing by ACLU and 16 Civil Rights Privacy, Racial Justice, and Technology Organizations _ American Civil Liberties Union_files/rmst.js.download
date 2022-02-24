var springboard = springboard || (function() {
    var _args = {},
        app_id = '',
        brand_url = '';

    return {
        init : function(Args) {
            _args = Args;
            brand_url = _args[0];
            app_id = _args[1];
            this.rmst();
        },

        rmst : function() {
            // Create an element to parse the URI.
            var uri = document.createElement('a');
            uri.href = location.href;

            if (uri.search) {
                // Get all query parameters from the url.
                var payload = this.parseQuery(uri.search.substr(1));

                // Include values from the url.
                var capture = ["protocol","hostname","port","pathname","hash"];
                capture.forEach(function(part) {
                    payload[part] = uri[part];
                });
                payload.referrer = document.referrer;

                // Arrange and encode the values into a string for the action url.
                var parts = [];
                Object.keys(payload).forEach(function(key) {
                  parts.push(encodeURIComponent(key) + '=' + encodeURIComponent(payload[key]));
                });
                var q = parts.join('&');

                var action = app_id + '/set?' + q;
                this.createTrackingPixel(action);
            }
        },

        parseQuery: function(query) {
            var result = {};
            query.split("&").forEach(function(part) {
                if(!part) return;
                part = part.split("+").join(" "); // replace every + with space, regexp-free version
                var eq = part.indexOf("=");
                var key = eq>-1 ? part.substr(0,eq) : part;
                var val = eq>-1 ? decodeURIComponent(part.substr(eq+1)) : "";
                var from = key.indexOf("[");

                if(from==-1) {
                    result[decodeURIComponent(key)] = val;
                }
                else {
                    var to = key.indexOf("]",from);
                    var index = decodeURIComponent(key.substring(from+1,to));
                    key = decodeURIComponent(key.substring(0,from));
                    if(!result[key]) result[key] = [];
                    if(!index) result[key].push(val);
                    else result[key][index] = val;
                }
            });

            return result;
        },

        createTrackingPixel: function(action) {
            (new Image()).src = (location.protocol == "https:" ? "https:" : "http:") + "//" + brand_url + "/" + action;
        }
    };
}());

var sbs = document.getElementById('springboard-jssdk');
var sbsq = sbs.src.replace(/^[^\?]+\??/, '');
var rmsInit = springboard.parseQuery(sbsq);
if (rmsInit['brand_url'] && rmsInit['app_id']) {
    springboard.init([rmsInit['brand_url'], rmsInit['app_id']]);
}
