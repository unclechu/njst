nJSt (Native JavaScript Templates)
==================================

Installing
----------

    npm install njst

Usage
-----

### template.html

    <html>
    <head>
        <title>%{page_title}</title>
    </head>

    <body>
        <h1>%{page_title}</h1>

        <ul>
        <% list.forEach(function (item) { %>
            <li>%{item}</li>
        <% }) %>
        </ul>

        <% if (show_message) { %>
            <p>nJSt loves you!</p>
        <% } %>
    </body>
    </html>

### test.js

    var path = require('path');
    var http = require('http');
    var njst = require('njst');

    var template = new njst();

    http.createServer(function (request, response) {
        var context = {
            page_title: 'nJSt demonstration',
            list: ['foo', 'bar', 'foobar'],
            show_message: true
        };

        template.renderFile(path.join(path.dirname(module.filename), 'template'), context, function (err, out) {
            if (err) {
                res.writeHead(500, {'Content-Type': 'text/plain; charset=utf-8'});
                res.end( err.toString() );
            }

            response.writeHead(200, {'Content-Type': 'text/html; charset=utf-8'});
            response.end(out);
        });
    }).listen(8000);

### Run

    node ./test.js

Authors
-------

Viacheslav Lotsmanov (unclechu)

See also
--------

https://github.com/visionmedia/ejs