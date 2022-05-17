# Magento2-Indexing

In Magento2 `Indexing` is used to transform data sush as products, categories to improve the performance of storefront. As data changes transformed data need to be updated/reindexed.

2 types of indexing in magento2 |---`Update on Schedule`
                                |
                                |---`Update on Save`
                                
  1. `Update on Schedule`:
         Indexing will take place when cron job is run.
         
         If there are 1 lakh products & if we change data of any 10 products. If indexing is set to update on schedule, how magento gets to know these are the 10 products for which indexing needs to be run?
                There is a mview.xml. There if we define indexer, we add subscription like which table. If any changes happened to that table then mysql triger will occour and that entity_id will go to the change log table like mviewId_cl table and change `indexer status` to `invalid`..In that table we have version_id, entity_id of the table. By using cron we can update the changed entity. There is a table called mview_state, there we get latest version_id.
                For every table listed in the table nodes, three types of MYSQL AFTER triggers are created: INSERT, UPDATE, DELETE.
         
  `Indexer status`: 
    1. valid - Ready - Data is synchronized, no reindex required.
    2. Invalid - Reindex required - Data is changed, index shoud be updated.
    3. Working - Processing - Indexing is in progress.
  
  The database status can be seen in SQL table 'indexer_state'.
  
  
 2. `Update on Save`:
          Whenever we change any data of entity & save immediately `indexing` will take place & update the date on the storefront.
          
 https://belvg.com/blog/index-management-in-magento-2.html
 

   ![index_indexers_flow](https://user-images.githubusercontent.com/46992129/168738037-6950b7fd-ab72-4c7f-a1b8-b8fe1526e542.png)
   
   
   
   
