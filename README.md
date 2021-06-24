# QISKIT for each result of mesurement  
qc=QuantumCircuit(2,2)
qc.h(0)
qc.cx(0, 1)
qc.measure([0,1],[0,1])
backend=Aer.get_backend('qasm_simulator')
option={'method':'statevector','memory':True}
result=execute(qc,backend,backend_options=option,shots=1024).result()
mem=result.get_memory(qc)
print(mem)
#
