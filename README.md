# checking
<?php

namespace Drupal\custom_queues\Plugin\QueueWorker;

use Drupal\Core\Entity\EntityTypeManagerInterface;
use Drupal\Core\Queue\QueueWorkerBase;

/**
* Processes queued items using batch processing.
*
* @QueueWorker(
* id = "node_update_queue",
* title = @Translation("Node Queue Worker"),
* cron = {"time" = 60}
* )
*/
class NodeUpdateQueue extends QueueWorkerBase {

public function processItem($data) {

  $node = \Drupal\node\Entity\Node::load($data['nid']);
  if ($node) {
    $node->setTitle($data['title']);
    $node->save();
  }
    
}   

}