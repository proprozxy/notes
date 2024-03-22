### ROS Usage

initialize

```bash
source /opt/ros/noetic/setup.bash
```

```bash
roscore
```

load config - run in a new terminal 

```bash
rviz -d rviz_config.rviz 
```

play rosbag in loop - run in another new terminal

```bash
rosbag play --loop /path/to/bag/file.bag
```

check topic for bag

```bash
rosbag info /path/to/bag/file.bag 
```



extract topic from rosbag into json file

```python
import json
import os
import rosbag
import argparse


def extract_messages_to_json(input_dir, topic_name, output_dir):
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)
    for root, dirs, files in os.walk(input_dir):
        for file in files:
            if file.endswith(".bag"):
                bag_path = os.path.join(root, file)
                print(f"Processing: {bag_path}")
                try:
                    bag = rosbag.Bag(bag_path, "r")
                    messages = []
                    for _, msg, _ in bag.read_messages(topics=[topic_name]):
                        # type(msg): std_msgs/String
                        # type(msg.data): String
                        dict_data = eval(msg.data) # dict_keys(['timestamp','trackable'])
                        # dict_data['trackable']: list
                        # dict_data['trackable'][0]: dict ; dict_keys(['id', 'position', 'dimension', 'heading', 'color'])
                        messages.append(dict_data)
                    if output_dir:
                        output_file_name = os.path.splitext(os.path.basename(bag_path))[0] + ".json"
                        json_path = os.path.join(output_dir, output_file_name)
                    else:
                        json_path = os.path.splitext(bag_path)[0] + ".json"
                    with open(json_path, "w") as json_file:
                        json.dump(messages, json_file)
                    print(f"Data extracted to: {json_path}")
                except Exception as e:
                    print(f"Error processing {bag_path}: {e}")
                finally:
                    bag.close()


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--bag_path', type=str, default='/home/curium/rosbag')
    parser.add_argument('--output_path', type=str, default='/home/curium/rosbag/json')
    parser.add_argument('--topic', type=str, default='/fusion_cloud/bbox/tracker_bbox_raw')
    args = parser.parse_args()

    bag_path = args.bag_path
    out_path = args.output_path
    topic_name = args.topic

    extract_messages_to_json(bag_path, topic_name, out_path)


if __name__ == "__main__":
    main()

```

