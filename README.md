## ERNIE + Select Knowledge

## 配置apex
> 必须设置为 --fp16，否则还有问题

```shell script
git clone https://github.com/NVIDIA/apex.git && \   
cd apex && \                                        
git checkout 5b71d3695bf39 && \                     
python setup.py install --cuda_ext --cpp_ext 
```

### 如果遇到gcc报错
> 将版本升级到7

```shell script
yum install centos-release-scl
yum install devtoolset-7-gcc-c++
source /opt/rh/devtoolset-7/enable
# 验证
gcc -v
```