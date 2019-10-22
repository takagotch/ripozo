### ripoze
---
https://github.com/vertical-knowledge/ripozo

```py
// ripozo_tests/integration/manager_base.py
from __future__ import absolute_import

import mock

from ripozo.resources.fields.base import BaseField
from ripozo.manager_base import BaseManager
from ripozo_tests.helpers.inmemory_manager import InMemoryManager

class TestManager(unittest2.TestCase):
  @property
  def manager(self):
    return InMemoryManager()
    
  @property
  def does_not_exist_exception(self):
    return KeyError
  
  @property
  def all_person_models(self):
    return list(six.intervalues(self._manager.objects))
  
  def get_person_model_by_id(self, person_id):
    return self._manager.objects[person_id]
    
  def test_field_validators(self):
    class MyManager(InMemoryManager):
      get_field_type = mock.MagicMock()
      pass
    self.assertIsNone(MyManager._field_validators)
    self.assertListEqual(MyManager.field_validators, [])
    
    class MyManager(MyManager):
      fields = [1, 2, 3]
    
    fields = MyManager.fields
    
    mck_list = MyManager.field_validators
    self.assertIsInstance(mck_list, list)
    self.assertEqual(MyManager.get_field_type.call_count, len(fields))
    args = list((x[0][0] for x in MyManager.get_field_type.call_args_list))
    self.assertListEqual(args, fields)

  def test_list_fields_property(self):
    _fields = [1, 2, 3]
    _list_fields = [4, 5]
    
    class m1(InMemoryManager):
      fields = _fields
      list_fields = _list_fields
    
    self.assertListEqual(_list_fields, M1.list_fields)
    self.assertListEqual(_fields, M1.fields)
    self.assertNotEqual(M1.list_fields, M1.fields)

    class M2(InMemoryManager):
      fields = _fields
      
    self.assertListEqual(_fields, M2.fields)
    self.assertListEqual(_fields, M2.list_fields)
    self.assertListEqual(M2.fields, M2.list_fields)

  def test_abstract_method_pissing_me_offf(self):
    class Manager(InMemoryManager):
      pass
    
    self.assertIsInstance(super(Manager, Manager()).get_field_type('blah'), BaseFiled)
  
  def test_update_fields(self):
    class Manager(InMemoryManager):
      fields = ('id', 'another', final)
    
    self.assertTupleEqual(Manager.fields, Manager.update_fields)
  
```

```
```

```
```
