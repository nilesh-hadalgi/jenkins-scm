# ubi minimal image
FROM registry.access.redhat.com/ubi8/ubi-minimal

# Labels
LABEL name="awsvmscheduler" \
    maintainer="tech@mycompany.com" \
    vendor="mycompany" \
    version="1.0.0" \
    release="1" \
    summary="This service enables AWS cloud vm start/stop." \
    description="This service enables AWS cloud vm start/stop."



ENV ec2_instanceIds ""
ENV ec2_command "start"

# copy bin file

COPY ./Nilesh/jenkins-files/AWSVMScheduler /AWSVMScheduler
#COPY AWSVMScheduler AWSVMScheduler

CMD ["sh", "-c", "./AWSVMScheduler -c  $ec2_command -i $ec2_instanceIds "]
