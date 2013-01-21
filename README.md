Simple python code that allows a connection to a carbon-cache sever for graphite.
This can be used as a python library or a standalone executable.

from the command line...
--------------------------

    ./carbonclient.py -m filesystem._root -v 53
    ./carbonclient.py -c cabonserver.example.com -p 2003 -g production -s myservername -m df_root -v 53
    ./carbonclient.py -c cabonserver.example.com -p 2003 -g production -s myservername -m df_root -v $( df -k / | awk '{print $5}' | sed 's/[^0-9]//g' | tail -1 )

from python - single update
----------------------------

    >>> from carbonclient import update
    >>> update(metric = "filesystem._root", value = 53)
    >>> update(server = "cabonserver.example.com", port = 2003, group = "production", metric = "filesystem._root", value= 53 )
    >>> update(server = "cabonserver.example.com", port = 2003, group = "production", metric = "filesystem._root", value= get_df('/') )


from python - bulk update: 
---------------------------

This takes a dictionary then cuts it up into updates of 500 and submits it as a multi-line update

    >>> from carbonclient import bulkupdate
    >>> data={'metric_name1': 123, 'metric_name2': 456, 'metric_name3': 789, 'metric_nameN': 1234}
    >>> bulkupdate(server = "carbon.example.com", port = 2003, group = "production", data = data)


GPL License
------------

    Simple python code that allows a connection to a carbon-cache sever for graphite.
    Copyright (C) 2013 Daniel Lawrence <dannyla@linux.com>

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.