# README

import os
import tarfile
from datetime import datetime
import sys

def archive_logs(log_directory):
    # Check if the provided log directory exists
    if not os.path.exists(log_directory):
        print(f"Error: The directory '{log_directory}' does not exist.")
        return

  # Create a new directory to store the archived logs
   archive_directory = "archived_logs"
   if not os.path.exists(archive_directory):
   os.makedirs(archive_directory)

  # Generate the name for the tar.gz file based on the current date and time
   timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
   archive_name = f"logs_archive_{timestamp}.tar.gz"
   archive_path = os.path.join(archive_directory, archive_name)

  # Compress the logs into a tar.gz file
   with tarfile.open(archive_path, "w:gz") as tar:
   tar.add(log_directory, arcname=os.path.basename(log_directory))

   # Log the date and time of the archive to a file
  log_file = os.path.join(archive_directory, "archive_log.txt")
  with open(log_file, "a") as log:
  log.write(f"{datetime.now()} - Archived logs to {archive_name}\n")

  print(f"Logs from '{log_directory}' have been archived to '{archive_path}'.")

if __name__ == "__main__":
    # Check if the user provided the log directory as an argument
    if len(sys.argv) != 2:
        print("Usage: log-archive <log-directory>")
        sys.exit(1)

  log_dir = sys.argv[1]
  archive_logs(log_dir)

# URL del Project: 
URL: https://github.com/EliLJ/README
