# Create virtual environment
And install packages in requirements.txt
```
pip install -r requirements.txt
```


# Download, transform, pickle datasets
Also pickle a DictVectorizer 
```
python preprocess_data.py --raw_data_path data_links.json --dest_path ./output
```

This will download datasets directly from [TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) without the need to actual download the parquets.

After this command, you should see an `./output` dir whose content look like this:

```
|-- [150K]  dv.pkl
|-- [2.5M]  test.pkl
|-- [2.0M]  train.pkl
`-- [2.2M]  val.pkl
```

# Run experiments
```
mlflow server --backend-store-uri sqlite:///backend.db --default-artifact-root ./artifacts
```
to tell `mlflow` to store artifacts in ./artifacts


## First experiment: train.py

Run 
```
python train.py
```

## Second experiment: optuna

Run
```
python hpo.py
```

## Test & Register the best model

```
python register_model.py
```
