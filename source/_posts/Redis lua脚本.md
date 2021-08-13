### Redis lua脚本

指令：

eval lua-script key-num

redis.call(command,key[param1,param2])

eval "redis.call('set',KEYS[1],ARGV[1])" 1 qs 2673