# This is code to extract results from the Noki "Evacuate" prompt, process, and display

It currently must be run from Dan's laptop.

To do everything type:

python downloadStorms.py; python processEvacuate.py; ./deploy_analysis.sh

Then in a few minutes, it should show up at

https://dosgoodcu.github.io/Evacuate/evacuation_results.html

But the caching is tricky and you may need to open a new incognito window

Or, if you want to be tricky, try adding dates
python processEvacuate.py  --end 2025-08-01

Or

python downloadStorms.py;  python processEvacuate.py  --Today ; ./deploy_analysis.sh

# Notes on how I did this are below.  Please note that some of these things are failed attempts.

Noki builder
https://fist-noki.iri.columbia.edu/
Username: noki_admin
Password: NokiCol@1754_DESDR
GUEST_USER = 'noki_guest'
GUEST_PWD = 'Noki_DESDR'

Building from email below…Make sure google docs uses simple " not right quotes
curl -X POST https://fist-noki.iri.columbia.edu/token \
     -H "Content-Type: application/json" \
     -d '{"username":"noki_admin","password":"NokiCol@1754_DESDR"}'

The token below comes from the command above…

curl -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTc2Nzk5NDE3MywianRpIjoiODA4YTkyMWYtMGQzNy00ZjM4LWI3ZWEtODY5ZmM1NTc5MGRmIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6Im5va2lfYWRtaW4iLCJuYmYiOjE3Njc5OTQxNzMsImV4cCI6MTc2ODAwNDk3M30.dMuWwuNAFICjhp2JziPbyuHa4pk0mhE_6oDy0LpCt2k" \
  -o NokiOutput.csv \
  "https://fist-noki.iri.columbia.edu/download_csv?deployment_name=Scored%20storms"

Used Gemini to make python code in ~/nokitestprocess that 
Downloads evacuation game:
python downloadStorms.py
Generates NokiEvacuateOutput.csv
Calculates plots of interesting choices, including html (player_breakdown.png, evacuation_overall.png, evacuation_by_type.png, and plots_summary.html)
python processEvacuate.py
Should have a –-today flag, but not sure how to test with only me
This functions: python processEvacuate.py --start 2025-01-10 --end 2025-09-09
Need to verify that the plots are correct!

Works!


curl -H "Authorization: Bearer <token>"  -o NokiOutput.csv "https://fist-noki.iri.columbia.edu/download_csv?deployment_name=storms"

On Dec 11, 2025, at 8:00 AM, Lilita Getnet Yenew <lgy2104@columbia.edu> wrote:

Hi Dan,
Hope you're doing well! Yes, we do have API endpoints in noki.py that can return a CSV. To use it, you’ll first generate an access token using your account. In a terminal, you would run:

curl -X POST https://<NOKI-SERVER-URL>/token \
     -H "Content-Type: application/json" \
     -d '{"username":"<your-username>","password":"<your-password>"}'

This will return a JSON response containing a "token" value. Copy that token and use it in the next command:

curl -H "Authorization: Bearer <your-token>" \
     -o <your-file-name>.csv \
     "https://<NOKI-SERVER-URL>/download_csv?deployment_name=NOKI"

That will save the file in your current folder. I haven't used this endpoint to extract CSVs myself yet, but based on the backend code, this is how it’s designed to work. If anything doesn’t behave as expected, or if you have any questions, I’d be happy to troubleshoot. Thank you!


Temporary Noki user guide
https://docs.google.com/document/d/1swTwjRUFirfAnfZnKdVtn9BTy0joJcw3vid-emhUeY4/edit?pli=1&tab=t.0

