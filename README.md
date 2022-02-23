HIFT_ENTER.

Listing 1: Use the Flot Javascript plotting library in Python
import json
import uuid
from IPython.display
    import display_javascript, display_html, display

class FlotPlot(object):
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.uuid = str(uuid.uuid4())

    def _ipython_display_(self):
        json_data = json.dumps(list(zip(self.x, self.y)))
        display_html(
            '<div id="{}" 
                style="height: 300px;
                width:80%;"></div>'
            .format(self.uuid), raw=True)
        display_javascript("""require(["..removed../jquery.flot.min.js"],

function() {
    var line = JSON.parse ("%s");
    console.log(line);
    $.plot("#%s", [line]);
});

""" % (json_data, self.uuid), raw=
