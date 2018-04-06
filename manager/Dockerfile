FROM golang
RUN : && \
    go get k8s.io/api/apps/v1beta1 && \
    go get k8s.io/api/core/v1 && \
    go get k8s.io/apimachinery/pkg/apis/meta/v1 && \
    go get k8s.io/client-go/kubernetes && \
    go get k8s.io/client-go/tools/clientcmd && \
    go get k8s.io/client-go/util/homedir && \
    go get k8s.io/client-go/util/retry && \
    go get k8s.io/client-go/rest && \
    go get k8s.io/apimachinery/pkg/runtime/serializer && \
    go get database/sql && \
    go get github.com/golang/protobuf/jsonpb && \
    go get github.com/go-sql-driver/mysql && \
    go get github.com/mattn/go-sqlite3 && \
    go get google.golang.org/grpc && \
    go get github.com/sirupsen/logrus && \
    go get github.com/docker/docker/api/types && \
    go get github.com/docker/docker/api/types/container && \
    go get github.com/docker/docker/client && \
    :
RUN apt update && apt install -y python python-pip
RUN pip install modeldb
ADD api $GOPATH/src/github.com/kubeflow/hp-tuning/api
ADD db $GOPATH/src/github.com/kubeflow/hp-tuning/db
ADD manager $GOPATH/src/github.com/kubeflow/hp-tuning/manager
ADD dlk $GOPATH/src/github.com/kubeflow/hp-tuning/dlk
ADD earlystopping $GOPATH/src/github.com/kubeflow/hp-tuning/earlystopping
ADD conf /conf
ADD manager/wrap.sh /wrap.sh
RUN chmod 755 /wrap.sh
WORKDIR $GOPATH/src/github.com/kubeflow/hp-tuning/manager
RUN go build -o vizier-manager