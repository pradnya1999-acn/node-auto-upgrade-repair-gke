provider "google" {
#   version = "= 3.55.0"
  credentials = var.sa_key
  project = "parabolic-base-409505"
}
 
variable "sa_key" {
  default =  ""
}

resource "google_container_cluster" "primary" {
  name     = "my-gke-cluster"
  location = "us-central1"

  node_pool {
    name = "default-node-pool"

    node_config {
      preemptible  = false
      machine_type = "n1-standard-1"

      oauth_scopes = [
        "https://www.googleapis.com/auth/logging.write",
        "https://www.googleapis.com/auth/monitoring",
      ]
    }

    #management {
    #  auto_repair  = false
     # auto_upgrade = false
    #}
  }

}
