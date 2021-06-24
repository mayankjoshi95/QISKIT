# QISKIT program for AER simulator
qc=QuantumCircuit(2,2)
qc.h(0)
qc.cx(0, 1)
qc.measure([0,1],[0,1])
backend=Aer.get_backend('qasm_simulator')
option={'method':'statevector','memory':True}
result=execute(qc,backend,backend_options=option,shots=1024).result()
mem=result.get_memory(qc)
print(mem)

#Intialize  with different state vector other than|00>
import numpy as np
qc1=QuantumCircuit(2,2)
intial=[0,1]
qc1.initialize([1/np.sqrt(5),0,0,2/np.sqrt(5)],intial)
qc1.measure([0,1],[0,1])
qc1.decompose()
qc1.draw()

#state vector reperesentation 
from qiskit import*
import numpy as np
from qiskit.visualization import plot_histogram
qc1=QuantumCircuit(4,4)
inial=[1,2,3]
qc1.initialize([0,0,0,1/np.sqrt(2),0,0,0,1/np.sqrt(2)],inial)
qc1.barrier()
for i in range(4):
    qc1.x(i)
qc1.cx(1,0)
qc1.measure(range(4),range(4))
qc1.draw()
backend=Aer.get_backend('statevector_simulator')
result=execute(qc1,backend,shots=1024).result()
statevector=result.get_statevector(qc1)
statevector


#to view both imaginary and real component of state vector

from qiskit import*
import numpy as np
from qiskit.visualization import plot_state_city
qc1=QuantumCircuit(4,4)
inial=[1,2,3]
qc1.initialize([0,0,0,1/np.sqrt(2),0,0,0,1/np.sqrt(2)],inial)
qc1.barrier()
for i in range(4):
    qc1.x(i)
qc1.cx(1,0)
qc1.h(3)
qc1.h(2)
qc1.measure(range(4),range(4))
qc1.draw()
backend=Aer.get_backend('statevector_simulator')
result=execute(qc1,backend,shots=1024).result()
count=result.get_statevector(qc1)
plot_state_city(count)



