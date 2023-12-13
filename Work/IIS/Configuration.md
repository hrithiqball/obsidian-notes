### Application Pool

To ensure the application is always running, 
1. Go to application pool on left side panel and double click it
2. Find the application pool name in the list and right click it
3. Open `Advanced Settings...`
	1. In **General** tab, click `Start Mode` and set it to `AlwaysRunning`
	2. In **Recycling** tab, set `Regular Time Interval(minutes)` to 0
4. Restart the application pool
