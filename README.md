# cordon

OpenShift - Cordon ve Drain İşlemleri
Bu doküman, OpenShift üzerinde cordon ve drain işlemlerinin nasıl yapılacağını açıklar. Bu işlemler genellikle bakım veya node taşıma gibi durumlarda kullanılır.

📝 Cordon İşlemi
Cordon işlemi, bir node'u yeni pod'ların atanmasına kapatır. Ancak, mevcut pod'lar çalışmaya devam eder.

Cordon İşlemi Nasıl Yapılır?
Node listesini görüntüleme:

oc get nodes
Node'u cordon yapma:

oc adm cordon <node-ismi>

Örnek:
oc adm cordon worker-node-1
Durumu kontrol etme:

oc get nodes
Çıktı:

pgsql

NAME             STATUS                     ROLES    AGE    VERSION
worker-node-1    Ready,SchedulingDisabled   worker   45d    v1.21.0
📝 Drain İşlemi
Drain işlemi, node üzerindeki tüm pod'ları boşaltır (başka node'lara taşır) ve node'u cordon durumuna alır.

Drain İşlemi Nasıl Yapılır?
Node'u drain yapma:

oc adm drain <node-ismi> --ignore-daemonsets --delete-local-data
Örnek:

bash
Copy
Edit
oc adm drain worker-node-1 --ignore-daemonsets --delete-local-data
Durumu kontrol etme:

oc get nodes
Çıktı:

NAME             STATUS                     ROLES    AGE    VERSION
worker-node-1    Ready,SchedulingDisabled   worker   45d    v1.21.0
Parametreler:

--ignore-daemonsets: DaemonSet pod'larını taşımadan bırakır.

--delete-local-data: Yerel geçici veriyi temizler.

📝 Node'u Tekrar Kullanıma Açma (Uncordon)
Drain veya cordon işlemi yapılmış bir node'u tekrar kullanılabilir hale getirmek için:

Uncordon işlemi:

oc adm uncordon <node-ismi>

Örnek:

oc adm uncordon worker-node-1
Durumu kontrol etme:

oc get nodes
Çıktı:

pgsql
NAME             STATUS    ROLES    AGE    VERSION
worker-node-1    Ready     worker   45d    v1.21.0
