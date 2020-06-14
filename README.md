# Smart-Queue-Monitoring-System

This is used to count people in manufacfturing,retail and transportation scenarios.it is developed using person-detection-retail-0013 model from the openvino pretrained model.It counts the number of people in the scene and draws bounding boxes around them.


In the 3 scenarios we use the follwing devices.FPGAs,VPU,CPU,GPU and after that we get to draw a graph and compare the hardwares.
 As a reminder, if you need to make any changes to the Python script, you can come back to this workspace to edit and run the above cell to overwrite the file with your changes.
 
How to run cpu
 
 #Submit job to the queue
cpu_job_id = !qsub queue_job.sh -d . -l nodes=1:tank-870:i5-6500te -F "/data/models/intel/person-detection-retail-0013/FP32/person-detection-retail-0013 CPU /data/resources/manufacturing.mp4 /data/queue_param/manufacturing.npy /output/results/manufacturing/CPU 2" -N store_core

print(cpu_job_id[0])

import liveQStat
liveQStat.liveQStat()


import get_results
get_results.getResults(cpu_job_id[0], filename='output.tgz', blocking=True)


!tar zxf output.tgz
!cat stdout.log

import videoHtml

videoHtml.videoHTML('Manufacturing CPU', ['results/manufacturing/CPU/output_video.mp4'])
