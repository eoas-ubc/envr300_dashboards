# Dashboards to explore time series for ENVR300

```
conda env create
conda activate envr300
python fetch_data.py
```

`fetch_data.py` Fetches data via ftp, filters NaN's and plots. That's all.
Output is `co2_fig.png`.

File `.\MonaLoaCO2\co2-mark3.md` is ready for DashBoard use. It was adapted from L. Heagey's tutorial by augmenting interactivity; i.e. by putting all useful adjustable parameters into widgets. File `1-widgets-an-example.md` is Lindsay's original. Other files in that folder are trial/error and learning efforts.

File `.\Vancouver-Ozone\O3-dataframes-and-bqplots.md` is NOT dashboard ready, but helps practice using dataframes and use of `bqplot` for interactivity. Other files are further trials/error. I will probably stop using `bqplot`, revert to "simpler" interactivity options, and focus this dashboard on ways of enabling students to explore "busy" data, smoothing and maximum daily 8 hour averages. This can also compare ozone at airport and mid-Fraser valley, which is interseting especially in summer. 

```python

```
