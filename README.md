# rtca
handling web activity data

һ�����軷����jvm1.7+��kafka 0.8.2.1��
����������ǰ������zookeeper��kafka��
����kafka�������ʹ���topic���£�
cd ��kafka Ŀ¼��
1.����kafka
./bin/kafka-server-start.sh -daemon config/server.properties
2.����topic
./bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 2 --topic topic-rtca
3.��֤�Ƿ񴴽��ɹ����Ƿ��������(��ѡ)
./bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic topic-rtca --from-beginning

��������������֣�
1��ca���֣�web���̣����Է���tomcat�����������У�
��Ҫ������˵����
kafka.zookeepers=192.168.3.102:2181 //zookeeper��ַ������ʵ�ʰ�װ��������
kafka.brokers=192.168.3.102:9092    //kafka��ַ������ʵ�ʰ�װ��������
kafka.groupId=grtca                 //kafka group���ƣ����ö�
kafka.topic=topic-rtca              //kafka topic���ƣ����ö�
zookeeper.connection.timeout.ms=10000 // zookeeper��ʱʱ�䣬���Բ��ö�
�����ʽmaven������ mvn clean install package -DskipTests

2.rtca����������Ŀ��������ʽ��./bin/start 192.168.3.102:2181 hbase001 10
����˵����
192.168.3.102:2181 Ϊzookeeper��ַ����ca�е����ñ���һ�£�
hbase001 hbase��ַ��������Ҫ����hbase����Щ���ļ���
10 Ϊ��ý���һ�������ռ�(�������һ��RDD)
���еڶ������ã�����ʵ�ʵ�hbase��װ���Լ����õ�host�ļ������趨
�����ʽsbt,���� sbt clean compile pack,Ϊtarget�µ�pack�ļ���

�������Է�ʽ����������Ͻ����������������в��ԣ�
�ġ������ص㣺
�����ܣ�
1.������������������bug��
2.���������ԣ���ԭϵͳ�е�����һ�£�
3.ϵͳ�쳣ʱ���ܴ��쳣�㿪ʼ�������ݽ��գ����ᶪʧ���ݣ�

�������ܣ�
������������⣬ÿ��֧��1100����������hbase
�ṩ���³�����ѹ������ͼ
1.������ͬ������Դʱ 
  1.��������ܱ仯���ߣ�����������Ӧʱ�䣬����������CPU���ڴ棬���̵Ȼ�����������ͼ��
  2.jvm�ڴ�仯���ߣ�
2.2X,3X,5X,10X����ѹ��ʱ������ָ�ꣻ


