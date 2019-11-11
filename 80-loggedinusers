#!/bin/bash
# This scripts prints out all logged in users
# Since these scripts will be executed before your session is initialized,
# it will return 0 for the first session and 1 for the second session
# So it displays the "other" logged in users.

echo ""
echo "logged in users:"
echo "  $(who|sed -e ':a;N;$!ba;s/\n/\n  /g')"
echo ""

