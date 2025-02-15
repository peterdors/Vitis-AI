# Run Customer Satisfaction Network

```sh
cd /workspace/vart/rnn-runner/apps/customer_satisfaction/

# [For U25]
sudo cp /workspace/vart/rnn-runner/xclbin/u25/dpu.xclbin /usr/lib/dpu.xclbin

# [For U50LV]
sudo cp /workspace/vart/rnn-runner/xclbin/u50lv/dpu.xclbin /usr/lib/dpu.xclbin
```

1. Download the model files
```sh
mkdir -p data/

cp /proj/rdi/staff/akorra/data/customer_satisfaction/complain_model.h5 data/

# [For U25]
cp ../../models/u25/xmodels-v1.0/lstm_customer_satisfaction/*.xmodel data/

# [For U50LV]
cp ../../models/u50/xmodels-v1.3/lstm_customer_satisfaction/*.xmodel data/
```

1. Get the datasets
```sh
# wget https://raw.githubusercontent.com/IBM/watson-machine-learning-samples/master/cloud/data/cars-4-you/car_rental_training_data.csv -P data/
cp /proj/rdi/staff/akorra/data/customer_satisfaction/car_rental_training_data.csv data
```

1. Setup the environment
```sh
source ./setup.sh
```

1. run the cpu mode with all trasactions
```sh
python run_cpu_e2e.py
```

1. run the dpu mode with all transactions
```sh
# For U25
TARGET_DEVICE=U25 python run_dpu_e2e.py

# For U50LV
TARGET_DEVICE=U50LV python run_dpu_e2e.py
```

1. run the dpu mode with multithread support
```sh
# For U25
TARGET_DEVICE=U25 python run_dpu_e2e_mt.py -n 4

# For U50LV
TARGET_DEVICE=U50LV python run_dpu_e2e_mt.py -n 4
```

1. The accuracy for the end-to-end model test should be: `0.9565`

#### License
Copyright 2021 Xilinx Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
