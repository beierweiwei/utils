var _ = require("lodash");

var param = function( a ) {
    var s = [], add = function( key, value ) {
        s[ s.length ] = encodeURIComponent(key) + "=" + encodeURIComponent(value);
    };
    for ( var prefix in a ) {
        buildParams( prefix, a[prefix], add );
    }
    return s.join("&").replace(/%20/g, "+");
};

var buildParams = function( prefix, obj, add ) {
    if ( _.isArray(obj) ) {
        _.forEach( obj, function( v, i ) {
            if ( /\[\]$/.test( prefix ) ) {
                add( prefix, v );
            } else {
                buildParams( prefix + "[" + ( typeof v === "object" || _.isArray(v) ? i : "" ) + "]", v, add );
            }
        });
    } else if ( obj != null && typeof obj === "object" ) {
        _.forEach( obj, function( v, k ) {
            buildParams( prefix + "[" + k + "]", v, add );
        });
    } else {
        add( prefix, obj );
    }
};
