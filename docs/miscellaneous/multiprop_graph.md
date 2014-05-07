# Tutorial on Using MultipropertyGraph in IBMPPL

1. Define graph type

```bash
   typedef ibmppl::ibm_multiproperty_persistent_graph graph_t;
   typedef ibmppl::ibm_multiproperty_inmemory_graph graph_t;

   typedef graph_t::vertex_iterator vit_t;
   typedef graph_t::edge_iterator   eit_t;
   typedef graph_t::pred_iterator   pred_t;
   typedef graph_t::vertexd_type    vid_t;
   typedef graph_t::edged_type	    eid_t;

   typedef int label_t;
````

1. Declare a graph

   graph_type g("name", "directory");

1. Add vertices

   label_t vlabel;
   vid_t vid = g.add_vertex(vlabel);

1. Add edges

   vid_t src, targ;
   label_t elabel;
   eid_t eid = g.add_edge(src, targ, elabel);

1. Find vertices

   vit_t vit = g.find_vertex(vid);
   vit_t vit = g.find_vertex(pkey, pval);

1. Find edges

   vid_t src, targ;
   eit_t eid;
   eit_t eit = g.find_edge(src, eid);  
   eit_t eit = g.find_edge(src, targ);   // need to add!!!

1. Property management

   string pkey, pval;
   vit->set_subproperty(pkey, pval);
   eit->set_subproperty(pkey, pval);
   
   string pval = vit->get_subproperty(pkey);
   string pval = eit->get_subproperty(ekey);

   size_t pid = get_vpropertyid(pkey);
   size_t pid = get_epropertyid(pkey);
   string pkey = get_vertex_property_name(pid);
   string pkey = get_edge_property_name(pid);
  
 
   // the following argment may be prop_id. should change to pkey!!!!

   vit->get_int_subproperty(pid);
   vit->get_double_subproperty(pid);
   time_t t = vit->get_time_subproperty(pid);

   int k = get_subpropertytype(pid);
   k = {CSVP_SUBPROPTYPE_STRING, CSVP_SUBPROPTYPE_INT, CSVP_SUBPROPTYPE_DOUBLE, CSVP_SUBPROPTYPE_TIME}

   g.delete_subproperty(pkey);
   g.delete_subproperty(pid);
   
   bool g.has_subproperty(pkey);

   size_t n = g.get_subproperty_count();

   

1. Traversal
   
   label_t lid;

   for (vit_t vit=g.vertices_begin(lid); vit!=g.vertices_end(lid); vit++)

   for (eit_t eit=vit.edges_begin(lid); eit!=vit.edges_end(lid); eit++)  // ???
   for (eit_t eit=vit->edges_begin(lid); eit!=vit->edges_end(lid); eit++)  // ???

   for (eit_t eit=vit.preds_begin(lid); eit!=vit.preds_end(lid); eit++)  // ???


1. Get number of edges for a vertex

   vit->edges_size(lid);
   vit->preds_size(lid);

1. Get end vertices of an edge

   eit->source();   // eit.source()??
   eit->target();
   eit_t eit = eit->id();

1. Deletion

   vid_t src, targ;
   g.delete_edge(src, targ);
    
