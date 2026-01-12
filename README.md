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
