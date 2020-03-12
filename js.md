    axios({method: 'GET', url: `${CONTACTS_URL}/previews/masters`}).catch(err => {
      console.log('err: ', err)
      return null
    }).then(res=>{
      let masterCols;
      console.log("res",res.data)
      new Promise((resolve, reject) => {
        try{
          masterCols=res.data.map(document=>{
            let notParent= document.keys.filter(key=>key.key!==key.parent)
            console.log(notParent);
            return notParent[0].key;
          })
        }catch(e){
          reject(e)
        }
        resolve(masterCols);
      }).then((notParentData) => {
        console.log(res)
        this.setState({masterData:notParentData})
      }).catch(e=>{
        console.log("error",e)
      })
    })
