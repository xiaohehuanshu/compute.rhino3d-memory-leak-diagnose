import compute_rhino3d.Util
import compute_rhino3d.Grasshopper as gh
import rhino3dm
import json
import pandas as pd
import numpy as np
import random

compute_rhino3d.Util.url = "http://localhost:8081/"


#comunicate with rhino
def environment(in_parm):
    
    #PATH1
    path1_px = gh.DataTree("RH_IN:PATH1_PX")
    path1_px.Append([0], [str(in_parm['path1'][0])])

    path1_py = gh.DataTree("RH_IN:PATH1_PY")
    path1_py.Append([0], [str(in_parm['path1'][1])])

    path1_dx = gh.DataTree("RH_IN:PATH1_DX")
    path1_dx.Append([0], [str(in_parm['path1'][2])])

    path1_dy = gh.DataTree("RH_IN:PATH1_DY")
    path1_dy.Append([0], [str(in_parm['path1'][3])])

    #PATH2
    path2_px = gh.DataTree("RH_IN:PATH2_PX")
    path2_px.Append([0], [str(in_parm['path2'][0])])

    path2_py = gh.DataTree("RH_IN:PATH2_PY")
    path2_py.Append([0], [str(in_parm['path2'][1])])

    path2_dx = gh.DataTree("RH_IN:PATH2_DX")
    path2_dx.Append([0], [str(in_parm['path2'][2])])

    path2_dy = gh.DataTree("RH_IN:PATH2_DY")
    path2_dy.Append([0], [str(in_parm['path2'][3])])

    #ROOM1
    room1_px = gh.DataTree("RH_IN:ROOM1_PX")
    room1_px.Append([0], [str(in_parm['room1'][0])])

    room1_py = gh.DataTree("RH_IN:ROOM1_PY")
    room1_py.Append([0], [str(in_parm['room1'][1])])

    room1_dx = gh.DataTree("RH_IN:ROOM1_DX")
    room1_dx.Append([0], [str(in_parm['room1'][2])])

    room1_dy = gh.DataTree("RH_IN:ROOM1_DY")
    room1_dy.Append([0], [str(in_parm['room1'][3])])

    #data trees
    trees = [
        path1_px, path1_py, path1_dx, path1_dy,
        path2_px, path2_py, path2_dx, path2_dy,
        room1_px, room1_py, room1_dx, room1_dy,
    ]

    output = gh.EvaluateDefinition('Diagnose.gh',trees) 

    #decode results
    branch = output['values']

    for item in branch:

        if item['ParamName'] == 'RH_OUT:SPACIAL_INFO':   
            out = item['InnerTree']['{ 0; }']
            spacial_relation = json.loads(out[0]['data'])

        else:
            pass
        
    return spacial_relation

#iterations
for iteration in range(100):       
    
    #generate random state
    random_num = np.random.randint(1,20, [4,4])*300
    STATE = pd.DataFrame(random_num, columns = ['boundary', 'path1', 'path2', 'room1'])
    
    #renewal parameters
    out_env = environment(in_parm = STATE)
    
    if iteration % 5 == 0:
        print(iteration)
