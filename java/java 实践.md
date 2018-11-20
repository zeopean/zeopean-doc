

### 生成签名算法：

```

    function generateSignature1($reqParamArrayWithSecret){
        // 1、 检验是否是数组
        if(!is_array($reqParamArrayWithSecret)){
            return "";   //不是数组返回空字符串
        }
        // 2、对数组进行排序
        sort($reqParamArrayWithSecret,2);
        // 3、对排序后的数组遍历 拼接字符串
        $str = "";
        foreach ($reqParamArrayWithSecret as $value) {
            $str .= $value;
        }
        // 4、进行sha1加密
        $sha1Str = sha1($str);
        //5、得到最后签名
        return $sha1Str;
    }
    

```

	

### java 多线程
	

* demo 1
	
```
	
	
private void MuitlThreadStat(List<Date> listDate, int count) {
        // 多线程执行 todo
        ExecutorService pool = Executors.newFixedThreadPool(8);
        CountDownLatch latch = new CountDownLatch(8);

        for (int i = 0; i < 8; i++) {
            final int tmp = i;
            Runnable runnable = new Runnable() {
                @Override
                public void run() {
                    try {
                        Date date = listDate.get(tmp + count);
                        // 按渠道统计
                        statByChannelHandler(date);

                        // 按测评统计
                        statByCepingHandler(date);
                    } finally {
                        // 有线程进来, 减1
                        latch.countDown();
                    }
                }
            };
            pool.submit(runnable);
        }
        try {
            latch.await();
            LOG.info("stat-success!");
        } catch (InterruptedException e) {
            LOG.info(e.getMessage());
        }
    }


```


* demo 2

```
        for (Date date : listDate) {
      
            executor.execute(new Runnable() {

                @Override
                public void run() {

                    // 按渠道统计
                    statByChannelHandler(date);

                    // 按测评统计
                    statByCepingHandler(date);

                }
            });
        }
        try {
            latch.await();
            LOG.info("stat-success!");
        } catch (InterruptedException e) {
            LOG.info(e.getMessage());
        }
```

* demo 3	
	
```

        for (Date date : listDate) {
            Runnable runnable = new Runnable() {
                @Override
                public void run() {
                    try {
                        // 按渠道统计
                        statByChannelHandler(date);

                        // 按测评统计
                        statByCepingHandler(date);
                    } finally {
                        // 有线程进来, 减1
                        latch.countDown();
                    }
                }
            };
            pool.submit(runnable);

        try {
            latch.await();
            LOG.info("stat-success!");
        } catch (InterruptedException e) {
            LOG.info(e.getMessage());
        }

```	


### java	排序

```

    /**
     * 排序
     *
     * @param lists
     * @param sort
     * @return
     */
    private List<StatCepingVo> sortStatCepingVos(List<StatCepingVo> lists, int sort) {

        Collections.sort(lists, new Comparator<StatCepingVo>() {
            @Override
            public int compare(StatCepingVo o1, StatCepingVo o2) {
                int sortAbs = Math.abs(sort);
                int res = 0;
                if (sortAbs == 1) {
                    if (sort > 0)
                        res = o2.getCreateCounts() - o1.getCreateCounts();
                    else
                        res = o1.getCreateCounts() - o2.getCreateCounts();
                } else if (sortAbs == 2) {
                    if (sort > 0)
                        res = o2.getPayCounts() - o1.getPayCounts();
                    else
                        res = o1.getPayCounts() - o2.getPayCounts();

                } else if (sortAbs == 3) {
                    if (sort > 0)
                        res = o2.getCompleteCounts() - o1.getCompleteCounts();
                    else
                        res = o1.getCompleteCounts() - o2.getCompleteCounts();

                } else if (sortAbs == 4) {
                    double price2 = Double.parseDouble(o2.getTotalPrice());
                    double price1 = Double.parseDouble(o1.getTotalPrice());
                    int iprice2 = MoneyUtils.changeY2F(price2);
                    int iprice1 = MoneyUtils.changeY2F(price1);
                    if (sort > 0) {
                        res = iprice2 - iprice1;
                    } else {
                        res = iprice1 - iprice2;
                    }
                }
                return res;
            }
        });

        return lists;
    }
    

```
	