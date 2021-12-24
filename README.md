## ERNIE + Select Knowledge

## 配置apex
> 必须设置为 --fp16，否则还有问题。
> 以下方案基于基本镜像venus-std-ext-cuda10.0-py3.6-tf2.0-pytorch1.2:1.0.0，
> 如果使用其他镜像可能有问题

```shell script
git clone https://github.com/NVIDIA/apex.git && \   
cd apex && \                                        
git checkout 5b71d3695bf39 && \                     
python setup.py install --cuda_ext --cpp_ext 
# 验证
# python
# from apex.fp16_utils.fp16_optimizer import FP16_Optimizer
# from apex.optimizers import FusedAdam
```

### 如果遇到gcc报错
> 将版本升级到7

```shell script
yum install centos-release-scl
yum install devtoolset-7-gcc-c++
source /opt/rh/devtoolset-7/enable
# 验证
# gcc -v
```

## finetune
如果已经有了输出文件，需要先删除
```shell script
rm -r output_fewrel
```

```shell script
nohup python3 code/run_fewrel.py \
--do_train \
--do_lower_case \
--data_dir data/fewrel/ \
--ernie_model ernie_base \
--max_seq_length 256 \
--train_batch_size 32 \
--learning_rate 2e-5 \
--num_train_epochs 10 \
--output_dir output_fewrel \
--loss_scale 128 > task.log 2>&1 &
```

--fp16 \